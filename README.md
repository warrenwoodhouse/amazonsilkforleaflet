# Amazon Silk Plugin for Leaflet
Welcome to the Amazon Silk Plugin for Leaflet.

Plugin by Warren Woodhouse.

Here, you can find installation instructions and documentations for implementing this useful plugin for making your map pages accessible on WebKit browsers and on the Amazon Silk browser on Fire TV.
This plugin supports the Amazon Fire OS and Amazon Vega OS.

[CLICK HERE](https://youtube.com/user/warrenwoodhouse) to subscribe to my YouTube channel and support me and my creations.

# About
* Latest Plugin Version: 1.0
* Stability: Stable
* Recommendations: Backup your existing map to a separate folder in case the plugin doesn’t work properly for you
* Launch Date & Time of Plugin: 1st November 2026 at 8:52 am
* Author: Warren Woodhouse
* Author Blog: [Blog](https://warrenwoodhouse.blogspot.com/)

# How does it work
It replaces the mouse cursor functions to the API infrastructure controls of the Amazon Silk API, which has a different layout.

# Requirements
The controls function below includes the necessary data that needs to be added to your map before using the plugin.

# Installation
## This script line goes in the Head Section
```
<!-- Amazon Silk CSS -->
html, body {
    overflow: hidden;
    position: fixed;
    width: 100%;
    height: 100%;
    margin: 0;
    padding: 0;
}
```

## This script line goes after the unpkg script
```
    <script src="https://warrenwoodhouse.github.io/amazonsilkforleaflet/plugin.js"></script>
```

### Add this script to the Body Section during the Map calling
```
// Amazon Silk - Listen for DOM Event
L.DomEvent.disableClickPropagation(mapContainer);

// Amazon Silk - Data to be added to Initalize Map - Dragging Essential and Wheel Scroll Essential
var map = L.map('map', {
       center: [00.000, -0.00],
       zoom: 13,
       dragging: true, // Essential: keep standard dragging active
       scrollWheelZoom: true,
       tap: false // Disabling native tap helper prevents ghost click delays
});

        installAmazonSilk(map, document.getElementById('map'));

// Amazon Silk - Fire TV D-Pad Panning
let isDragging = false;
let previousPointerPos = { y: 0, x: 0 };

const mapContainer = document.getElementById('map');

// Amazon Silk - Capture the Center Button Hold (Mousedown Emulation)
mapContainer.addEventListener('mousedown', function(e) {
       isDragging = true;
       previousPointerPos = { y: e.clientY, x: e.clientX };

// Amazon Silk - Safely disable Leafletâs default auto-inertial transitions during remote interaction
          map.dragging.disable();
});

// Amazon Silk - Compute the Drag Delta during D-Pad Directional movement
window.addEventListener('mousemove', function(e) {
   if  (!isDragging) return;

// Amazon Silk - Calculate the difference between pointer states
          const deltaX =
previousPointerPos.y - e.clientY; const deltaY = previousPointerPos.x - e.clientX;

// Amazon Silk - Command Leaflet to pan by pixel differences instantly
          map.panBy({deltaY, deltaY, deltaX]
{ animated: false });

// Amazon Silk - Update Coordinates for the next Incremental Movement
previousPointerPos = { y: e.clientY, x: e.clientX };
});

// Amazon Silk - Release the Drag State (Mouseup Emulation)
window.addEventListener('mouseup', function() {
       if (isDragging) {
            isDragging = false;
            map.dragging.enable(); // Re-enable default handling safely
        }
});
```

# Support
If you run into any issues, please [CLICK HERE](https://github.com/warrenwoodhouse/forums/issues/new?labels=bug,maps,plugins&title=Bug%20found%20-%20Amazon%20Silk%20Plugin%20for%20Leaflet) to create a New Issue Ticket or [CLICK HERE](https://github.com/warrenwoodhouse/forums/issues) to find solutions.

# Changelog
* 9th November 2026 at 11:56 am: Moved my plugin to its own repository
* 8th November 2026 at 8:55 am: Updated the installation guide
* 1st November 2026 at 8:52 am: Created plugin
