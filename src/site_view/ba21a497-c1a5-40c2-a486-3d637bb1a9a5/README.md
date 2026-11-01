### JCB! Site View
# Occupancy map (occupancy_map)

Map of occupancy of locations

## HTML:
```html
<?php
/** @var Joomla\CMS\WebAsset\WebAssetManager $wa */
$wa = $this->getDocument()->getWebAssetManager();
$wa->useScript('keepalive')->useScript('form.validate');
Html::_('bootstrap.tooltip');
?>

<?php
// -------------------------------------------------------------------------
// 1. RECOVERY & CALCULATION OF DYNAMIC PRESENCES FROM DATABASE
// -------------------------------------------------------------------------

$app   = Factory::getApplication();
$input = $app->getInput();

// Intervallo di date selezionato dall'utente (Default: da oggi a +14 giorni)
$startDateInput = $input->getString('start_date', date('Y-m-d'));
$endDateInput   = $input->getString('end_date', date('Y-m-d', strtotime('+14 days')));

// Controllo validità intervallo
if (strtotime($startDateInput) > strtotime($endDateInput)) {
    $endDateInput = $startDateInput;
}

$db = Factory::getContainer()->get('DatabaseDriver');

// STEP A: Recupero delle Location e relative Coordinate da Place
$queryPlaces = $db->getQuery(true)
    ->select([
        $db->quoteName('l.id', 'location_id'),
        $db->quoteName('l.place_id', 'place_id'),
        $db->quoteName('l.name', 'loc_name'),
        $db->quoteName('l.location', 'loc_title'),
        $db->quoteName('p.place', 'place_name'),
        $db->quoteName('p.latitude', 'latitude'),
        $db->quoteName('p.longitude', 'longitude')
    ])
    ->from($db->quoteName('#__bookings_location', 'l'))
    ->innerJoin($db->quoteName('#__bookings_place', 'p') . ' ON ' . $db->quoteName('l.place_id') . ' = ' . $db->quoteName('p.id'));

$db->setQuery($queryPlaces);
$locationsList = $db->loadObjectList() ?: [];

// Struttura base delle location e mappa delle chiavi di ricerca
$baseLocations = [];
$lookupMap     = [];

foreach ($locationsList as $loc) {
    $locId   = (string) $loc->location_id;
    $placeId = (string) $loc->place_id;
    
    $displayName = !empty($loc->place_name) ? $loc->place_name : (!empty($loc->loc_name) ? $loc->loc_name : $loc->loc_title);

    $baseLocations[$locId] = [
        'location_id' => (int) $loc->location_id,
        'place_id'    => (int) $loc->place_id,
        'place_name'  => $displayName,
        'lat'         => (float) $loc->latitude,
        'lng'         => (float) $loc->longitude,
    ];

    // 1. Collega direttamente l'ID della Location al proprio ID Location
    $lookupMap['loc_' . $locId] = $locId;
    $lookupMap[$locId]         = $locId;

    // 2. Collega l'ID del Place all'ID Location corrispondente
    if (!empty($placeId)) {
        $lookupMap['place_' . $placeId] = $locId;
        if (!isset($lookupMap[$placeId])) {
            $lookupMap[$placeId] = $locId;
        }
    }
    
    // 3. Mappatura flessibile per nomi/titoli sia del Place che della Location
    foreach ([$loc->place_name, $loc->loc_name, $loc->loc_title] as $nameCandidate) {
        if (!empty($nameCandidate)) {
            $trimmed = trim($nameCandidate);
            $lookupMap[$trimmed]                = $locId;
            $lookupMap[mb_strtolower($trimmed)] = $locId;
        }
    }
}

// STEP B: Recupero prenotazioni che intersecano la finestra di date (fino a 10 giorni prima)
$queryRes = $db->getQuery(true)
    ->select('*')
    ->from($db->quoteName('#__bookings_reservation'))
    ->where('DATE(' . $db->quoteName('datefirststop') . ') <= ' . $db->quote($endDateInput))
    ->where('DATE(' . $db->quoteName('datefirststop') . ') >= DATE_SUB(' . $db->quote($startDateInput) . ', INTERVAL 9 DAY)');

$db->setQuery($queryRes);
$reservations = $db->loadObjectList() ?: [];

// STEP C: Calcolo Presenze Giorno per Giorno
$timelineData = [];
$currentDt    = new DateTime($startDateInput);
$endDt        = new DateTime($endDateInput);

while ($currentDt <= $endDt) {
    $dateStr = $currentDt->format('Y-m-d');
    
    // Inizializza presenze azzerate per la data corrente
    $dayOccupancy = [];
    foreach ($baseLocations as $locId => $baseInfo) {
        $dayOccupancy[$locId] = array_merge($baseInfo, [
            'total_participants' => 0,
            'groups'             => []
        ]);
    }

    foreach ($reservations as $res) {
        if (empty($res->datefirststop) || $res->datefirststop === '0000-00-00') {
            continue;
        }

        $pax       = (int) ($res->participants ?? 0);
        $groupName = !empty($res->group) ? $res->group : (!empty($res->id_code) ? $res->id_code : 'Gruppo Sconosciuto');

        // Calcola a quale stop corrisponde la data corrente
        $resStart = new DateTime($res->datefirststop);
        $diffDays = (int) $resStart->diff($currentDt)->format("%r%a");
        $activeStopIndex = $diffDays + 1; // 1-based index (Giorno 0 = stop_01)

        if ($activeStopIndex >= 1 && $activeStopIndex <= 10) {
            // Genera il nome esatto della colonna: stop_01, stop_02, ..., stop_10
            $colName = 'stop_' . sprintf('%02d', $activeStopIndex);
            $rawVal  = $res->$colName ?? null;

            if (!empty($rawVal)) {
                // Pulizia se memorizzato come JSON
                if (is_string($rawVal) && (strpos($rawVal, '[') === 0 || strpos($rawVal, '{') === 0)) {
                    $decoded = json_decode($rawVal, true);
                    if (is_array($decoded)) {
                        $rawVal = reset($decoded);
                    }
                }

                $cleanVal = is_string($rawVal) ? trim($rawVal) : (string) $rawVal;
                $lowerVal = is_string($rawVal) ? mb_strtolower($cleanVal) : $cleanVal;

                $matchedKey = $lookupMap[$cleanVal] 
                           ?? $lookupMap['place_' . $cleanVal] 
                           ?? $lookupMap['loc_' . $cleanVal] 
                           ?? $lookupMap[$lowerVal] 
                           ?? null;

                if ($matchedKey && isset($dayOccupancy[$matchedKey])) {
                    $dayOccupancy[$matchedKey]['total_participants'] += $pax;
                    $dayOccupancy[$matchedKey]['groups'][] = [
                        'name' => $groupName,
                        'pax'  => $pax,
                        'stop' => $activeStopIndex
                    ];
                }
            }
        }
    }

    $timelineData[$dateStr] = array_values($dayOccupancy);
    $currentDt->modify('+1 day');
}

$jsonTimeline = json_encode($timelineData);
?>

<!-- ----------------------------------------------------------------------- -->
<!-- 2. LEAFLET CSS & JS DEPENDENCIES + CUSTOM STYLES                        -->
<!-- ----------------------------------------------------------------------- -->
<link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />
<script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>

<style>
/* Stile per i pallini numerici */
.circle-number-marker {
    background: transparent !important;
    border: none !important;
}

.circle-number-badge {
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 50%;
    color: #ffffff;
    font-weight: bold;
    font-size: 13px;
    border: 2px solid #ffffff;
    box-shadow: 0 2px 6px rgba(0,0,0,0.4);
    transition: all 0.3s ease;
    user-select: none;
}
</style>

<!-- ----------------------------------------------------------------------- -->
<!-- 3. HTML VIEW LAYOUT                                                     -->
<!-- ----------------------------------------------------------------------- -->
<div class="container-fluid p-0">
    <!-- Form Filtro Date -->
    <div class="card mb-3">
        <div class="card-body py-2">
            <form id="map-range-form" method="get" class="row align-items-end g-3">
                <input type="hidden" name="option" value="com_bookings">
                <input type="hidden" name="view" value="occupancy_map">

                <div class="col-auto">
                    <label for="start_date" class="form-label fw-bold">Data Inizio:</label>
                    <input type="date" id="start_date" name="start_date" class="form-control" 
                           value="<?php echo htmlspecialchars($startDateInput, ENT_QUOTES, 'UTF-8'); ?>">
                </div>

                <div class="col-auto">
                    <label for="end_date" class="form-label fw-bold">Data Fine:</label>
                    <input type="date" id="end_date" name="end_date" class="form-control" 
                           value="<?php echo htmlspecialchars($endDateInput, ENT_QUOTES, 'UTF-8'); ?>">
                </div>

                <div class="col-auto">
                    <button type="submit" class="btn btn-secondary">
                        Imposta Intervallo
                    </button>
                </div>
            </form>
        </div>
    </div>

    <!-- Controlli Player Animazione -->
    <div class="card mb-3 border-primary">
        <div class="card-body bg-light py-2">
            <div class="row align-items-center">
                <div class="col-md-4">
                    <div class="d-flex align-items-center gap-2">
                        <button id="btn-play" class="btn btn-success btn-lg">▶ Play</button>
                        <button id="btn-pause" class="btn btn-warning btn-lg" disabled>⏸ Pause</button>
                        <button id="btn-reset" class="btn btn-outline-secondary">🔄 Reset</button>
                    </div>
                </div>
                <div class="col-md-5 text-center">
                    <h3 class="m-0 text-primary fw-bold" id="current-date-display">
                        📅 <?php echo htmlspecialchars($startDateInput, ENT_QUOTES, 'UTF-8'); ?>
                    </h3>
                </div>
                <div class="col-md-3">
                    <input type="range" class="form-range" id="timeline-slider" min="0" value="0" step="1">
                </div>
            </div>
        </div>
    </div>

    <!-- Map Container -->
    <div class="card">
        <div class="card-body p-0">
            <div id="occupancy-map" style="height: 650px; width: 100%; border-radius: 4px;"></div>
        </div>
    </div>
</div>

<!-- ----------------------------------------------------------------------- -->
<!-- 4. JAVASCRIPT ANIMATED MAP ENGINE                                       -->
<!-- ----------------------------------------------------------------------- -->
<script>
document.addEventListener('DOMContentLoaded', function () {
    var timelineData = <?php echo $jsonTimeline; ?>;
    var dates = Object.keys(timelineData);
    
    if (dates.length === 0) return;

    var currentIndex = 0;
    var timer = null;
    var markersMap = {};

    // Coordinate di default (Nord Italia / Alpi)
    var map = L.map('occupancy-map').setView([46.2000, 9.5000], 9);

    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
        maxZoom: 19,
        attribution: '&copy; OpenStreetMap contributors'
    }).addTo(map);

    var playBtn = document.getElementById('btn-play');
    var pauseBtn = document.getElementById('btn-pause');
    var resetBtn = document.getElementById('btn-reset');
    var dateDisplay = document.getElementById('current-date-display');
    var slider = document.getElementById('timeline-slider');

    slider.max = dates.length - 1;

    // Calcola il diametro in px del cerchio in base al numero di persone
    function calculateSize(pax) {
        if (pax === 0) return 24;
        var size = 26 + Math.sqrt(pax) * 5; 
        return Math.min(Math.round(size), 60);
    }

    // Determina il colore di sfondo in base alla capienza/afflusso
    function calculateColor(pax) {
        if (pax === 0)  return '#6c757d';  // Grigio (Vuoto)
        if (pax <= 25) return '#198754';  // Verde (Basso)
        if (pax <= 35) return '#fd7e14';  // Arancione (Medio)
        if (pax >  35) return '#dc3545';  // Rosso (Alto)
        return '#8b0000';                // Rosso Scuro (Molto Alto)
    }

    // Genera l'HTML del marcatore circolare con il numero inserito al centro
    function createCircleMarkerIcon(pax) {
        var size = calculateSize(pax);
        var color = calculateColor(pax);

        var html = '<div class="circle-number-badge" style="' +
            'width:' + size + 'px; ' +
            'height:' + size + 'px; ' +
            'background-color:' + color + ';' +
            '">' + pax + '</div>';

        return L.divIcon({
            className: 'circle-number-marker',
            html: html,
            iconSize: [size, size],
            iconAnchor: [size / 2, size / 2]
        });
    }

    // Inizializza i marcatori Leaflet
    var initialDate = dates[0];
    var initialLocations = timelineData[initialDate];
    var bounds = [];

    initialLocations.forEach(function (loc) {
        if (!loc.lat || !loc.lng) return;
        bounds.push([loc.lat, loc.lng]);

        var pax = loc.total_participants;

        var marker = L.marker([loc.lat, loc.lng], {
            icon: createCircleMarkerIcon(pax),
            zIndexOffset: pax > 0 ? 1000 + pax : 0 // Se pax > 0 va in primo piano
        }).addTo(map);

        markersMap[loc.location_id] = marker;
    });

    if (bounds.length > 0) {
        map.fitBounds(bounds, { padding: [50, 50] });
    }

    // Renderizza lo stato per la data selezionata nell'indice
    function renderDateIndex(index) {
        var dateStr = dates[index];
        var locations = timelineData[dateStr];

        dateDisplay.innerHTML = '📅 ' + dateStr;
        slider.value = index;

        locations.forEach(function (loc) {
            var marker = markersMap[loc.location_id];
            if (!marker) return;

            var pax = loc.total_participants;

            // Aggiorna l'icona circolare con dimensione, colore e testo variati
            marker.setIcon(createCircleMarkerIcon(pax));

            // Gestisce la priorità visiva (z-index): 0 va sullo sfondo, >0 in primo piano
            marker.setZIndexOffset(pax > 0 ? 1000 + pax : 0);

            // Popup HTML informativo al click
            var popupHtml = '<div style="min-width: 180px;">';
            popupHtml += '<h5 style="margin: 0 0 5px 0;">' + (loc.place_name || 'Location') + '</h5>';
            popupHtml += '<div style="margin-bottom:5px;"><strong>Data: </strong>' + dateStr + '</div>';
            popupHtml += '<div><strong>Presenze Totali: </strong><span class="badge bg-secondary">' + pax + '</span></div>';
            popupHtml += '<hr style="margin: 8px 0;">';

            if (loc.groups.length > 0) {
                popupHtml += '<strong>Gruppi Presenti:</strong><ul style="padding-left: 18px; margin: 4px 0;">';
                loc.groups.forEach(function (g) {
                    popupHtml += '<li><b>' + g.name + '</b>: ' + g.pax + ' pax (Stop #' + g.stop + ')</li>';
                });
                popupHtml += '</ul>';
            } else {
                popupHtml += '<span style="color: #6c757d;">Nessuna presenza registrata.</span>';
            }
            popupHtml += '</div>';

            marker.bindPopup(popupHtml);
        });
    }

    function play() {
        if (timer) return;
        playBtn.disabled = true;
        pauseBtn.disabled = false;

        timer = setInterval(function () {
            currentIndex++;
            if (currentIndex >= dates.length) {
                currentIndex = dates.length - 1;
                pause();
                return;
            }
            renderDateIndex(currentIndex);
        }, 1000); // 1 secondo per ogni giorno
    }

    function pause() {
        if (timer) {
            clearInterval(timer);
            timer = null;
        }
        playBtn.disabled = false;
        pauseBtn.disabled = true;
    }

    function reset() {
        pause();
        currentIndex = 0;
        renderDateIndex(currentIndex);
    }

    // Event listeners per controlli
    playBtn.addEventListener('click', play);
    pauseBtn.addEventListener('click', pause);
    resetBtn.addEventListener('click', reset);

    slider.addEventListener('input', function () {
        pause();
        currentIndex = parseInt(this.value, 10);
        renderDateIndex(currentIndex);
    });

    // Renderizza il primo giorno all'avvio
    renderDateIndex(0);
});
</script>
```

> Deliver dynamic, custom front-end experiences with this reusable Site View crafted for seamless data flow and design flexibility in JCB.

### Used in [Joomla Component Builder](https://www.joomlacomponentbuilder.com) - [Source](https://git.vdm.dev/joomla/Component-Builder) - [Mirror](https://github.com/vdm-io/Joomla-Component-Builder) - [Download](https://git.vdm.dev/joomla/pkg-component-builder/releases)

---
[![Joomla Volunteer Portal](https://img.shields.io/badge/-Joomla-gold?logo=joomla)](https://volunteers.joomla.org/joomlers/1396-llewellyn-van-der-merwe "Join Llewellyn on the Joomla Volunteer Portal: Shaping the Future Together!") [![GitHub](https://img.shields.io/badge/-Git-181717?logo=git)](https://github.com/joomengine "Build premium Joomla extensions with JoomEngine on GitHub: Help us raise Joomla extension standards!") [![Octoleo](https://img.shields.io/badge/-Octoleo-black?logo=linux)](https://git.vdm.dev/octoleo "--quiet") [![Llewellyn](https://img.shields.io/badge/-Llewellyn-ffffff?logo=gitea)](https://git.vdm.dev/Llewellyn "Collaborate and Innovate with Llewellyn on Git: Building a Better Code Future!") [![Telegram](https://img.shields.io/badge/-Telegram-blue?logo=telegram)](https://t.me/Joomla_component_builder "Join Llewellyn and the Community on Telegram: Building Joomla Components Together!") [![Mastodon](https://img.shields.io/badge/-Mastodon-9e9eec?logo=mastodon)](https://joomla.social/@llewellyn "Connect and Engage with Llewellyn on Joomla Social: Empowering Communities, One Post at a Time!") [![X (Twitter)](https://img.shields.io/badge/-X-black?logo=x)](https://x.com/llewellynvdm "Join the Conversation with Llewellyn on X: Where Ideas Take Flight!") [![GitHub](https://img.shields.io/badge/-GitHub-181717?logo=github)](https://github.com/Llewellynvdm "Build, Innovate, and Thrive with Llewellyn on GitHub: Turning Ideas into Impact!") [![YouTube](https://img.shields.io/badge/-YouTube-ff0000?logo=youtube)](https://www.youtube.com/@OctoYou "Explore, Learn, and Create with Llewellyn on YouTube: Your Gateway to Inspiration!") [![n8n](https://img.shields.io/badge/-n8n-black?logo=n8n)](https://n8n.io/creators/octoleo "Effortless Automation and Impactful Workflows with Llewellyn on n8n!") [![Docker Hub](https://img.shields.io/badge/-Docker-grey?logo=docker)](https://hub.docker.com/r/octoleo/joomengine "JoomEngine on Docker: Containerize Your Creativity!") [![Open Collective](https://img.shields.io/badge/-Donate-green?logo=opencollective)](https://opencollective.com/joomla-component-builder "Donate towards JCB: Help Llewellyn financially so he can continue developing this great tool!") [![GPG Key](https://img.shields.io/badge/-GPG-blue?logo=gnupg)](https://git.vdm.dev/Llewellyn/gpg "Unlock Trust and Security with Llewellyn's GPG Key: Your Gateway to Verified Connections!")