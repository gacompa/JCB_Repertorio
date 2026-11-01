### JCB! Site View
# Places map (places_map)

Display of places map

## HTML:
```html
<style>
    #map-container {
        height: 800px;
        width: 100%;
        border-radius: 8px;
        box-shadow: 0 4px 6px rgba(0,0,0,0.1);
        margin-top: 20px;
    }
</style>

<div id="map-container"></div>

<script>
document.addEventListener('DOMContentLoaded', function() {
    // Check if Leaflet is loaded
    if (typeof L === 'undefined') {
        console.error("Leaflet library not loaded.");
        return;
    }

    const map = L.map('map-container').setView([20, 0], 2); // A general view of the world

    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
        attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
    }).addTo(map);
    // Aggiungi il layer con curve di livello
    var topoLayer = L.tileLayer('https://{s}.tile.opentopomap.org/{z}/{x}/{y}.png', {
        maxZoom: 17,
        attribution: 'Map data: &copy; OpenStreetMap contributors, SRTM | Map style: &copy; OpenTopoMap (CC-BY-SA)'
    }).addTo(map);

    // Get the locations from PHP and parse them into a JavaScript object.
    const places = <?php echo json_encode($this->items); ?>;
    const markers = [];

    places.forEach(function(place) {
        // Ensure latitude and longitude are valid numbers
        const lat = parseFloat(place.latitude);
        const lng = parseFloat(place.longitude);

        if (!isNaN(lat) && !isNaN(lng)) {
        const markerOptions = {
            radius: 10,           // Increased size for visibility
            fillColor: "#ff0000",   // Red color
            color: "#ffffff",   // Outline color (white creates a "halo" effect)
            weight: 2,            // Thickness of the outline
            opacity: 1,           // Opacity of the outline
            fillOpacity: 0.9,     // Makes the color more solid
            pane: 'markerPane',   // Ensures markers stay above the map layers
            interactive: true,    // Set to false if you want the marker to be "ghost"
            className: 'pulsing-marker' // Add a CSS class for animations            radius: 8,
        };
        const marker = L.circleMarker([lat, lng], markerOptions).addTo(map);

        // Use bindTooltip for "hover" behavior
        // 'sticky: true' makes the tooltip follow the mouse cursor
        marker.bindTooltip(`<b>${escapeHtml(place.place)}</b><br>Alt: ${escapeHtml(place.altitude)}m`, {
            permanent: false, 
            direction: 'top',
            sticky: true,
            className: 'custom-tooltip' // Optional: for custom CSS
            }
        );
        // You can still keep bindPopup for "click" behavior if you want both
        marker.bindPopup(`Full details for ${escapeHtml(place.place)}...`);
        markers.push(marker);
        }
        }
    );


    if (markers.length > 0) {
        // Fit the map view to show all markers
        const group = new L.featureGroup(markers);
        map.fitBounds(group.getBounds().pad(0.5));
    }
});
function escapeHtml(text) {
    if (!text) return text;
    const div = document.createElement('div');
    div.textContent = text;
    return div.innerHTML;
}
</script>
```

> Deliver dynamic, custom front-end experiences with this reusable Site View crafted for seamless data flow and design flexibility in JCB.

### Used in [Joomla Component Builder](https://www.joomlacomponentbuilder.com) - [Source](https://git.vdm.dev/joomla/Component-Builder) - [Mirror](https://github.com/vdm-io/Joomla-Component-Builder) - [Download](https://git.vdm.dev/joomla/pkg-component-builder/releases)

---
[![Joomla Volunteer Portal](https://img.shields.io/badge/-Joomla-gold?logo=joomla)](https://volunteers.joomla.org/joomlers/1396-llewellyn-van-der-merwe "Join Llewellyn on the Joomla Volunteer Portal: Shaping the Future Together!") [![GitHub](https://img.shields.io/badge/-Git-181717?logo=git)](https://github.com/joomengine "Build premium Joomla extensions with JoomEngine on GitHub: Help us raise Joomla extension standards!") [![Octoleo](https://img.shields.io/badge/-Octoleo-black?logo=linux)](https://git.vdm.dev/octoleo "--quiet") [![Llewellyn](https://img.shields.io/badge/-Llewellyn-ffffff?logo=gitea)](https://git.vdm.dev/Llewellyn "Collaborate and Innovate with Llewellyn on Git: Building a Better Code Future!") [![Telegram](https://img.shields.io/badge/-Telegram-blue?logo=telegram)](https://t.me/Joomla_component_builder "Join Llewellyn and the Community on Telegram: Building Joomla Components Together!") [![Mastodon](https://img.shields.io/badge/-Mastodon-9e9eec?logo=mastodon)](https://joomla.social/@llewellyn "Connect and Engage with Llewellyn on Joomla Social: Empowering Communities, One Post at a Time!") [![X (Twitter)](https://img.shields.io/badge/-X-black?logo=x)](https://x.com/llewellynvdm "Join the Conversation with Llewellyn on X: Where Ideas Take Flight!") [![GitHub](https://img.shields.io/badge/-GitHub-181717?logo=github)](https://github.com/Llewellynvdm "Build, Innovate, and Thrive with Llewellyn on GitHub: Turning Ideas into Impact!") [![YouTube](https://img.shields.io/badge/-YouTube-ff0000?logo=youtube)](https://www.youtube.com/@OctoYou "Explore, Learn, and Create with Llewellyn on YouTube: Your Gateway to Inspiration!") [![n8n](https://img.shields.io/badge/-n8n-black?logo=n8n)](https://n8n.io/creators/octoleo "Effortless Automation and Impactful Workflows with Llewellyn on n8n!") [![Docker Hub](https://img.shields.io/badge/-Docker-grey?logo=docker)](https://hub.docker.com/r/octoleo/joomengine "JoomEngine on Docker: Containerize Your Creativity!") [![Open Collective](https://img.shields.io/badge/-Donate-green?logo=opencollective)](https://opencollective.com/joomla-component-builder "Donate towards JCB: Help Llewellyn financially so he can continue developing this great tool!") [![GPG Key](https://img.shields.io/badge/-GPG-blue?logo=gnupg)](https://git.vdm.dev/Llewellyn/gpg "Unlock Trust and Security with Llewellyn's GPG Key: Your Gateway to Verified Connections!")