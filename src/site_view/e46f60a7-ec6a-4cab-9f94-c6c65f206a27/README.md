### JCB! Site View
# App Piece single (app_piece_single)

Show the data of a single piece

## HTML:
```html
<!--[JCBGUI.site_view.default.77.$$$$]-->
<div class="repertorio-single-column-wrapper container my-3" style="max-width: 650px; margin: 0 auto;">

    <!-- 1. Bottone "Torna alla ricerca" -->
    <?php $searchUrl = Route::_('index.php?option=com_repertorio&view=app_select_piece'); ?>
    <div class="back-to-search-wrapper mb-3">
        <a href="<?php echo htmlspecialchars($searchUrl, ENT_QUOTES, 'UTF-8'); ?>" class="back-to-search-btn">
            <span class="back-icon">←</span> Torna alla ricerca
        </a>
    </div>

    <!-- 2. Intestazione: Titolo e Autore del Pezzo -->
    <div class="piece-header-card p-3 mb-3 bg-white border rounded shadow-sm text-center">
        <h2 class="h4 mb-1 fw-bold text-primary"><?php echo htmlspecialchars($this->item->title ?? 'Brano senza titolo', ENT_QUOTES, 'UTF-8'); ?></h2>
        <?php if (!empty($this->item->author)) : ?>
            <p class="mb-0 text-muted">Compositore / Autore: <strong><?php echo htmlspecialchars($this->item->author, ENT_QUOTES, 'UTF-8'); ?></strong></p>
        <?php endif; ?>
    </div>

    <!-- 3. Sezione Audio e Parti Vocali -->
    <?php
    $sopranoLabel = !empty(trim((string)($this->item->soprano_label ?? $this->item->sopranolabel ?? ''))) 
                    ? ($this->item->soprano_label ?? $this->item->sopranolabel) : 'Soprano';

    $altoLabel    = !empty(trim((string)($this->item->alto_label ?? $this->item->altolabel ?? ''))) 
                    ? ($this->item->alto_label ?? $this->item->altolabel) : 'Contralto';

    $tenorLabel   = !empty(trim((string)($this->item->tenor_label ?? $this->item->tenorlabel ?? ''))) 
                    ? ($this->item->tenor_label ?? $this->item->tenorlabel) : 'Tenore';

    $bassLabel    = !empty(trim((string)($this->item->bass_label ?? $this->item->basslabel ?? ''))) 
                    ? ($this->item->bass_label ?? $this->item->basslabel) : 'Basso';

    $parts = [
        'soprano' => ['initial' => 'S', 'label' => $sopranoLabel, 'audio' => $this->item->soprano_part ?? '', 'youtube' => $this->item->soprano_part_yt ?? ''],
        'alto'    => ['initial' => 'A', 'label' => $altoLabel,    'audio' => $this->item->alto_part ?? '',    'youtube' => $this->item->alto_part_yt ?? ''],
        'tenor'   => ['initial' => 'T', 'label' => $tenorLabel,   'audio' => $this->item->tenor_part ?? '',   'youtube' => $this->item->tenor_part_yt ?? ''],
        'bass'    => ['initial' => 'B', 'label' => $bassLabel,    'audio' => $this->item->bass_part ?? '',    'youtube' => $this->item->bass_part_yt ?? ''],
    ];

    $partType = strtolower(trim((string) ($this->item->part_type ?: 'recording')));

    $availableAudioParts = [];
    if ($partType !== 'youtube') {
        foreach ($parts as $key => $part) {
            if (!empty($part['audio'])) {
                $availableAudioParts[] = [
                    'key'     => $key,
                    'initial' => $part['initial'],
                    'label'   => $part['label'],
                    'audioId' => 'audio-' . $key
                ];
            }
        }
    }
    ?>
    <script>
        window.availableAudioParts = <?php echo json_encode($availableAudioParts); ?>;
    </script>

    <div class="parts-section p-3 mb-3 bg-white border rounded shadow-sm">
        <h3 class="h6 fw-bold mb-3 text-secondary text-center">🎵 Seleziona la parte da ascoltare</h3>
        <?php $ytPointers = []; ?>
        <?php if ($partType === 'youtube') : ?>
        <div class="yt-pointer-grid">
        <?php endif; ?>
        <?php foreach ($parts as $key => $part) : ?>

            <?php if ($partType === 'youtube') : ?>
                <?php
                $videoId = RepertorioHelper::getYoutubeId($part['youtube']);
                if (!$videoId) { continue; }
                $ytPointers[] = ['key' => $key, 'label' => $part['label'], 'videoId' => $videoId];
                ?>
                <button type="button" class="yt-pointer-btn mb-2" data-yt-id="<?php echo htmlspecialchars($videoId, ENT_QUOTES, 'UTF-8'); ?>"
                        aria-label="Riproduci parte <?php echo htmlspecialchars($part['label'], ENT_QUOTES, 'UTF-8'); ?> su YouTube">
                    <span class="yt-pointer-icon">
                        <svg viewBox="0 0 68 48" xmlns="http://www.w3.org/2000/svg">
                            <path d="M66.52 7.74c-.78-2.93-2.49-5.41-5.42-6.19C55.79.13 34 0 34 0S12.21.13 6.9 1.55C3.97 2.33 2.26 4.81 1.48 7.74.06 13.05 0 24 0 24s.06 10.95 1.48 16.26c.78 2.93 2.49 5.41 5.42 6.19C12.21 47.87 34 48 34 48s21.79-.13 27.1-1.55c2.93-.78 4.64-3.26 5.42-6.19C67.94 34.95 68 24 68 24s-.06-10.95-1.48-16.26z" fill="#f00"/>
                            <path d="M27 34l18-10-18-10z" fill="#fff"/>
                        </svg>
                    </span>
                    <span class="yt-pointer-label"><?php echo htmlspecialchars($part['label'], ENT_QUOTES, 'UTF-8'); ?></span>
                </button>
            <?php else : ?>
                <?php if (empty($part['audio'])) : continue; endif; ?>
                <?php
                $audioId   = 'audio-' . $key;
                $cleanAudio = File::makeSafe((string) $part['audio']);
                $partsUrl  = Uri::root(true) . '/files/coro_della_svolta/parts/' . $cleanAudio;
                $partsUrlEsc  = htmlspecialchars($partsUrl, ENT_QUOTES, 'UTF-8');
                ?>
                <div class="part-audio-box p-2 mb-2 bg-light rounded border">
                    <div class="d-flex align-items-center gap-2">
                        <button type="button" class="part-play-btn" data-audio="<?php echo $audioId; ?>"
                                aria-label="Riproduci parte <?php echo htmlspecialchars($part['label'], ENT_QUOTES, 'UTF-8'); ?>">
                            <span class="play-icon">▶</span>
                        </button>
                        <div class="part-info flex-grow-1">
                            <span class="part-title fw-bold text-dark"><?php echo htmlspecialchars($part['label'], ENT_QUOTES, 'UTF-8'); ?></span>
                            <div class="part-progress-row d-flex align-items-center gap-2 mt-1">
                                <input type="range" class="part-progress form-range" data-audio="<?php echo $audioId; ?>"
                                       value="0" min="0" max="100" step="0.1">
                                <span class="part-time small text-muted" data-audio="<?php echo $audioId; ?>">0:00 / 0:00</span>
                            </div>
                        </div>
                    </div>
                    <audio id="<?php echo $audioId; ?>" preload="none" src="<?php echo $partsUrlEsc; ?>"></audio>
                </div>
            <?php endif; ?>
        <?php endforeach; ?>
        <?php if ($partType === 'youtube') : ?>
        </div>
        <?php endif; ?>
    </div>

    <?php if ($partType === 'youtube' && !empty($ytPointers)) : ?>
    <div class="yt-shared-player-section mb-3">
        <div class="yt-shared-player-wrapper" id="yt-shared-player-wrapper">
            <p class="yt-shared-placeholder" id="yt-shared-placeholder">Seleziona una parte qui sopra per avviare il video.</p>
            <iframe id="yt-shared-player" src="" title="Parte selezionata" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen style="display:none;"></iframe>
        </div>
    </div>
    <?php endif; ?>

    <!-- 4. Sezione Spartito PDF (Chiusa di default, apribile a comando) -->
    <?php 
        $cleanScore = File::makeSafe((string) ($this->item->score ?? ''));
        $pdfUrl     = Uri::root(true) . '/files/coro_della_svolta/scores/' . $cleanScore;
        $pdfUrlEsc  = htmlspecialchars($pdfUrl, ENT_QUOTES, 'UTF-8');
    ?>
    <?php if (!empty($cleanScore)) : ?>
    <div class="pdf-section mb-3">
        <button type="button" class="toggle-btn" id="pdf-toggle-btn"
                aria-expanded="false" aria-controls="pdf-wrapper">
            <span class="toggle-icon" id="pdf-toggle-icon">📄</span>
            <span id="pdf-toggle-label">Visualizza / Sfoglia Spartito PDF</span>
        </button>

        <div class="pdf-wrapper" id="pdf-wrapper" style="display: none;">
            <div class="pdf-viewer-container" id="pdf-viewer-container">
                <div class="pdf-toolbar">
                    <div class="pdf-nav-controls">
                        <button type="button" id="pdf-prev" class="pdf-btn">‹ Prec</button>
                        <span class="pdf-page-info">
                            Pag. <span id="pdf-page-num">1</span> di <span id="pdf-page-count">--</span>
                        </span>
                        <button type="button" id="pdf-next" class="pdf-btn">Succ ›</button>
                    </div>

                    <div class="pdf-zoom-controls">
                        <button type="button" id="pdf-zoom-in" class="pdf-btn-action" title="Ingrandisci (Zoom +)">➕</button>
                        <button type="button" id="pdf-zoom-out" class="pdf-btn-action" title="Riduci (Zoom -)">➖</button>
                        <button type="button" id="pdf-zoom-reset" class="pdf-btn-action" title="Ripristina dimensione">🔄</button>
                    </div>

                    <div class="pdf-actions">
                        <button type="button" id="pdf-fullscreen-btn" class="pdf-btn-action" title="Schermo intero">
                            <span class="action-icon">🔍</span> Ingrandisci
                        </button>
                        <a href="<?php echo $pdfUrlEsc; ?>" download class="pdf-download-circular-btn" target="_blank" rel="noopener" title="Scarica PDF originale">
                            <span class="download-icon">📥</span>
                        </a>
                    </div>
                </div>

                <div class="pdf-canvas-wrapper" id="flipbook-wrapper">
                    <div id="pdf-loading-msg" style="color: #fff; padding: 2rem;">Caricamento dello spartito sfogliabile...</div>
                    <div id="pdf-book"></div>
                </div>
            </div>
        </div>
    </div>
    <?php endif; ?>

    <!-- 5. Video Performance (Chiuso di default, apribile a comando) -->
    <?php 
        $publicVideoId = RepertorioHelper::getYoutubeId($this->item->public_performance ?? '');
        $videoUrl  = 'https://www.youtube.com/embed/' . $publicVideoId;
        $videoUrlEsc  = htmlspecialchars($videoUrl, ENT_QUOTES, 'UTF-8');
    ?>
    <?php if (!empty($publicVideoId)) : ?>
    <div class="video-section mb-3">
        <button type="button" class="toggle-btn toggle-btn-video" id="video-toggle-btn"
                aria-expanded="false" aria-controls="video-wrapper">
            <span class="toggle-icon" id="video-toggle-icon">🎬</span>
            <span id="video-toggle-label">Visualizza Video di Esecuzione</span>
        </button>

        <div class="video-wrapper p-3 bg-white border rounded shadow-sm mt-2" id="video-wrapper" style="display: none;">
            <div class="video-responsive-wrapper" style="position:relative; padding-top:56.25%;">
                <iframe id="public-performance-iframe" data-src="<?php echo $videoUrlEsc; ?>" src="" title="Performance Video" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen style="position:absolute; top:0; left:0; width:100%; height:100%;"></iframe>
            </div>
        </div>
    </div>
    <?php endif; ?>

</div>

<!-- Caricamento PDF.js v2.16.105 & StPageFlip via CDN -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/2.16.105/pdf.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/page-flip/dist/js/page-flip.browser.js"></script>

<script>
document.addEventListener('DOMContentLoaded', function () {
    var pdfjsLib = window['pdfjs-dist/build/pdf'];
    var pdfLoaded = false;

    // Toggle Spartito PDF
    var pdfToggleBtn   = document.getElementById('pdf-toggle-btn');
    var pdfWrapper     = document.getElementById('pdf-wrapper');
    var pdfToggleLabel = document.getElementById('pdf-toggle-label');

    if (pdfToggleBtn && pdfWrapper) {
        pdfToggleBtn.addEventListener('click', function () {
            var isHidden = pdfWrapper.style.display === 'none';
            pdfWrapper.style.display = isHidden ? 'block' : 'none';
            pdfToggleBtn.classList.toggle('is-expanded', isHidden);
            pdfToggleBtn.setAttribute('aria-expanded', isHidden ? 'true' : 'false');
            
            if (pdfToggleLabel) {
                pdfToggleLabel.textContent = isHidden ? 'Nascondi spartito' : 'Visualizza / Sfoglia Spartito PDF';
            }

            if (isHidden && !pdfLoaded && pdfjsLib) {
                pdfLoaded = true;
                initPdfViewer();
            }
        });
    }

    // Toggle Video di Esecuzione
    var videoToggleBtn   = document.getElementById('video-toggle-btn');
    var videoWrapper     = document.getElementById('video-wrapper');
    var videoToggleLabel = document.getElementById('video-toggle-label');
    var videoIframe      = document.getElementById('public-performance-iframe');

    if (videoToggleBtn && videoWrapper) {
        videoToggleBtn.addEventListener('click', function () {
            var isHidden = videoWrapper.style.display === 'none';
            videoWrapper.style.display = isHidden ? 'block' : 'none';
            videoToggleBtn.classList.toggle('is-expanded', isHidden);
            videoToggleBtn.setAttribute('aria-expanded', isHidden ? 'true' : 'false');

            if (videoToggleLabel) {
                videoToggleLabel.textContent = isHidden ? 'Nascondi Video di Esecuzione' : 'Visualizza Video di Esecuzione';
            }

            if (videoIframe) {
                if (isHidden) {
                    var dataSrc = videoIframe.getAttribute('data-src');
                    if (dataSrc) videoIframe.src = dataSrc;
                } else {
                    videoIframe.src = '';
                }
            }
        });
    }

    function initPdfViewer() {
        pdfjsLib.GlobalWorkerOptions.workerSrc = 'https://cdnjs.cloudflare.com/ajax/libs/pdf.js/2.16.105/pdf.worker.min.js';

        var url = '<?php echo $pdfUrlEsc; ?>';
        var bookContainer = document.getElementById('pdf-book');
        var loadingMsg = document.getElementById('pdf-loading-msg');
        var canvasWrapper = document.getElementById('flipbook-wrapper');
        var pageFlip = null;

        pdfjsLib.getDocument(url).promise.then(async function (pdfDoc) {
            var numPages = pdfDoc.numPages;
            document.getElementById('pdf-page-count').textContent = numPages;

            pageFlip = new St.PageFlip(bookContainer, {
                width: 400,
                height: 550,
                size: "stretch",
                minWidth: 260,
                maxWidth: 800,
                minHeight: 350,
                maxHeight: 1000,
                maxShadowOpacity: 0.4,
                showCover: true,
                mobileScrollSupport: true
            });

            var dpr = window.devicePixelRatio || 1;

            for (var pageNum = 1; pageNum <= numPages; pageNum++) {
                var page = await pdfDoc.getPage(pageNum);
                var viewport = page.getViewport({ scale: 1.2 * dpr });

                var pageDiv = document.createElement('div');
                pageDiv.className = 'page-slide';

                var canvas = document.createElement('canvas');
                var ctx = canvas.getContext('2d');

                canvas.height = viewport.height;
                canvas.width  = viewport.width;
                canvas.style.width  = '100%';
                canvas.style.height = '100%';

                pageDiv.appendChild(canvas);
                bookContainer.appendChild(pageDiv);

                await page.render({
                    canvasContext: ctx,
                    viewport: viewport
                }).promise;
            }

            if (loadingMsg) loadingMsg.style.display = 'none';

            pageFlip.loadFromHTML(document.querySelectorAll('.page-slide'));

            pageFlip.on('flip', (e) => {
                document.getElementById('pdf-page-num').textContent = e.data + 1;
            });

            document.getElementById('pdf-prev').addEventListener('click', function () {
                if (pageFlip) pageFlip.turnToPrevPage();
            });

            document.getElementById('pdf-next').addEventListener('click', function () {
                if (pageFlip) pageFlip.turnToNextPage();
            });

        }).catch(function (err) {
            console.error('Errore caricamento PDF Flipbook:', err);
            if (loadingMsg) loadingMsg.textContent = 'Errore durante il caricamento del PDF.';
        });
    }

    // CONTROLLI AUDIO TRACCE
    var buttons = document.querySelectorAll('.part-play-btn');

    buttons.forEach(function (btn) {
        var audioId = btn.getAttribute('data-audio');
        var audio   = document.getElementById(audioId);
        var icon    = btn.querySelector('.play-icon');

        if (!audio) return;

        btn.addEventListener('click', function () {
            if (audio.paused) {
                document.querySelectorAll('audio').forEach(function (a) {
                    if (a !== audio) a.pause();
                });
                audio.play();
            } else {
                audio.pause();
            }
        });

        function updateAudioStates(isPlaying) {
            if (isPlaying) {
                icon.textContent = '⏸';
                btn.classList.add('is-playing');
            } else {
                icon.textContent = '▶';
                btn.classList.remove('is-playing');
            }
        }

        audio.addEventListener('play',  function () { updateAudioStates(true); });
        audio.addEventListener('pause', function () { updateAudioStates(false); });
        audio.addEventListener('ended', function () { updateAudioStates(false); });

        var progress  = document.querySelector('.part-progress[data-audio="' + audioId + '"]');
        var timeLabel = document.querySelector('.part-time[data-audio="' + audioId + '"]');

        function formatTime(seconds) {
            if (isNaN(seconds)) return '0:00';
            var m = Math.floor(seconds / 60);
            var s = Math.floor(seconds % 60).toString().padStart(2, '0');
            return m + ':' + s;
        }

        audio.addEventListener('loadedmetadata', function () {
            timeLabel.textContent = formatTime(audio.currentTime) + ' / ' + formatTime(audio.duration);
        });

        audio.addEventListener('timeupdate', function () {
            if (audio.duration) {
                progress.value = (audio.currentTime / audio.duration) * 100;
            }
            timeLabel.textContent = formatTime(audio.currentTime) + ' / ' + formatTime(audio.duration);
        });

        progress.addEventListener('input', function () {
            if (audio.duration) {
                audio.currentTime = (progress.value / 100) * audio.duration;
            }
        });
    });
});
</script>

<style>
.repertorio-single-column-wrapper {
    width: 100%;
    box-sizing: border-box;
}

.piece-header-card {
    background: #ffffff;
    border-left: 4px solid #2e7d32 !important;
}

.part-audio-box {
    transition: background-color 0.2s;
}

.part-play-btn { 
    display: inline-flex; 
    align-items: center; 
    justify-content: center; 
    width: 2.8rem; 
    height: 2.8rem; 
    border-radius: 50%; 
    border: none; 
    background: #2e7d32; 
    color: #fff; 
    cursor: pointer; 
    font-size: 1.2rem; 
    flex-shrink: 0; 
}
.part-play-btn.is-playing { background: #d32f2f; }
.part-play-btn:hover { opacity: 0.9; }

.toggle-btn { 
    display: flex; 
    align-items: center; 
    justify-content: center;
    width: 100%;
    gap: 0.5rem; 
    padding: 0.8rem 1rem; 
    border: 2px solid #2e7d32; 
    border-radius: 8px; 
    background: #2e7d32; 
    color: #fff; 
    font-weight: bold;
    cursor: pointer; 
    font-size: 1rem; 
    box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}
.toggle-btn:hover { background: #1b5e20; }

.toggle-btn-video {
    border-color: #1976d2;
    background: #1976d2;
}
.toggle-btn-video:hover { background: #0d47a1; }

.pdf-viewer-container {
    display: flex;
    flex-direction: column;
    border: 1px solid #e0e0e0;
    border-radius: 8px;
    overflow: hidden;
    background: #f8f9fa;
    margin-top: 0.5rem;
}

.pdf-toolbar {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0.5rem;
    background: #323639;
    color: #fff;
    font-size: 0.85rem;
    flex-wrap: wrap;
    gap: 0.4rem;
}

.pdf-btn, .pdf-btn-action {
    background: #4a4d51;
    color: #fff;
    border: 1px solid #666;
    border-radius: 4px;
    padding: 0.3rem 0.6rem;
    cursor: pointer;
    font-size: 0.8rem;
}

.pdf-canvas-wrapper {
    display: block;
    overflow: auto;
    padding: 1rem 0.5rem;
    background: #525659;
    min-height: 350px;
    text-align: center;
}

#pdf-book {
    margin: 0 auto;
    display: inline-block;
}

.page-slide {
    background-color: #fff;
    box-shadow: 0 0 10px rgba(0,0,0,0.2);
}
.page-slide canvas {
    width: 100%;
    height: 100%;
}

.back-to-search-btn { 
    display: inline-flex; 
    align-items: center; 
    gap: 0.4rem; 
    padding: 0.4rem 0.9rem; 
    border: 1px solid #ccc; 
    border-radius: 999px; 
    background: #fff; 
    font-size: 0.9rem; 
    color: #333; 
    text-decoration: none; 
}
.back-to-search-btn:hover { background: #f2f2f2; }
</style>
<!--[/JCBGUI$$$$]-->

<!-- SCRIPT PER LA MEMORIZZAZIONE NEL LOCALSTORAGE (SOLO SU SELEZIONE VOCE) -->
<script>
document.addEventListener('DOMContentLoaded', function () {
    const pieceId = "<?php echo (int) ($this->item->id ?? 0); ?>";
    const pieceTitle = <?php echo json_encode($this->item->title ?? 'Brano'); ?>;
    const pieceComposer = <?php echo json_encode($this->item->author ?? ''); ?>;

    // Funzione per registrare la traccia e la voce specifica
    function saveRecentVoiceChoice(voiceLabel) {
        if (!pieceId || pieceId === "0" || !voiceLabel) return;

        let recentPieces = JSON.parse(localStorage.getItem('coro_recent_pieces') || '[]');
        
        // Chiave univoca basata su ID brano + Voce selezionata
        const currentKey = pieceId + '_' + voiceLabel;

        // Rimuove eventuali registrazioni identiche precedenti
        recentPieces = recentPieces.filter(item => (item.id + '_' + item.voice) !== currentKey);
        
        // Aggiunge in cima la nuova selezione con traccia e voce
        recentPieces.unshift({ 
            id: pieceId, 
            title: pieceTitle, 
            composer: pieceComposer,
            voice: voiceLabel 
        });
        
        // Conserva solo le ultime 3 selezioni
        if (recentPieces.length > 3) {
            recentPieces = recentPieces.slice(0, 3);
        }
        
        localStorage.setItem('coro_recent_pieces', JSON.stringify(recentPieces));
    }

    // Intercetta il click sui pulsanti Play delle parti audio e sui pulsanti parte YouTube
    const playButtons = document.querySelectorAll('.part-play-btn, .yt-pointer-btn');
    playButtons.forEach(function (btn) {
        btn.addEventListener('click', function () {
            let voiceLabel = '';
            
            // Estrae l'etichetta della voce (Soprano, Contralto, Tenore, Basso)
            const partBox = btn.closest('.part-audio-box');
            if (partBox) {
                const titleEl = partBox.querySelector('.part-title');
                if (titleEl) voiceLabel = titleEl.textContent.trim();
            } else {
                const ytLabel = btn.querySelector('.yt-pointer-label');
                if (ytLabel) voiceLabel = ytLabel.textContent.trim();
            }

            if (voiceLabel) {
                saveRecentVoiceChoice(voiceLabel);
            }
        });
    });
});
</script>
```

> Deliver dynamic, custom front-end experiences with this reusable Site View crafted for seamless data flow and design flexibility in JCB.

### Used in [Joomla Component Builder](https://www.joomlacomponentbuilder.com) - [Source](https://git.vdm.dev/joomla/Component-Builder) - [Mirror](https://github.com/vdm-io/Joomla-Component-Builder) - [Download](https://git.vdm.dev/joomla/pkg-component-builder/releases)

---
[![Joomla Volunteer Portal](https://img.shields.io/badge/-Joomla-gold?logo=joomla)](https://volunteers.joomla.org/joomlers/1396-llewellyn-van-der-merwe "Join Llewellyn on the Joomla Volunteer Portal: Shaping the Future Together!") [![GitHub](https://img.shields.io/badge/-Git-181717?logo=git)](https://github.com/joomengine "Build premium Joomla extensions with JoomEngine on GitHub: Help us raise Joomla extension standards!") [![Octoleo](https://img.shields.io/badge/-Octoleo-black?logo=linux)](https://git.vdm.dev/octoleo "--quiet") [![Llewellyn](https://img.shields.io/badge/-Llewellyn-ffffff?logo=gitea)](https://git.vdm.dev/Llewellyn "Collaborate and Innovate with Llewellyn on Git: Building a Better Code Future!") [![Telegram](https://img.shields.io/badge/-Telegram-blue?logo=telegram)](https://t.me/Joomla_component_builder "Join Llewellyn and the Community on Telegram: Building Joomla Components Together!") [![Mastodon](https://img.shields.io/badge/-Mastodon-9e9eec?logo=mastodon)](https://joomla.social/@llewellyn "Connect and Engage with Llewellyn on Joomla Social: Empowering Communities, One Post at a Time!") [![X (Twitter)](https://img.shields.io/badge/-X-black?logo=x)](https://x.com/llewellynvdm "Join the Conversation with Llewellyn on X: Where Ideas Take Flight!") [![GitHub](https://img.shields.io/badge/-GitHub-181717?logo=github)](https://github.com/Llewellynvdm "Build, Innovate, and Thrive with Llewellyn on GitHub: Turning Ideas into Impact!") [![YouTube](https://img.shields.io/badge/-YouTube-ff0000?logo=youtube)](https://www.youtube.com/@OctoYou "Explore, Learn, and Create with Llewellyn on YouTube: Your Gateway to Inspiration!") [![n8n](https://img.shields.io/badge/-n8n-black?logo=n8n)](https://n8n.io/creators/octoleo "Effortless Automation and Impactful Workflows with Llewellyn on n8n!") [![Docker Hub](https://img.shields.io/badge/-Docker-grey?logo=docker)](https://hub.docker.com/r/octoleo/joomengine "JoomEngine on Docker: Containerize Your Creativity!") [![Open Collective](https://img.shields.io/badge/-Donate-green?logo=opencollective)](https://opencollective.com/joomla-component-builder "Donate towards JCB: Help Llewellyn financially so he can continue developing this great tool!") [![GPG Key](https://img.shields.io/badge/-GPG-blue?logo=gnupg)](https://git.vdm.dev/Llewellyn/gpg "Unlock Trust and Security with Llewellyn's GPG Key: Your Gateway to Verified Connections!")