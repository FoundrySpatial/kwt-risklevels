<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Display a map on a webpage</title>
<meta name="viewport" content="initial-scale=1,maximum-scale=1,user-scalable=no">
<link href="https://api.mapbox.com/mapbox-gl-js/v2.5.0/mapbox-gl.css" rel="stylesheet">
<script src="https://api.mapbox.com/mapbox-gl-js/v2.5.0/mapbox-gl.js"></script>
<style>
body { margin: 0; padding: 0; }
#map { position: absolute; top: 0; bottom: 0; width: 100%; }
</style>
</head>
<body>
	<style>
#menu {
background: #fff;
position: absolute;
z-index: 1;
top: 10px;
right: 10px;
border-radius: 3px;
width: 120px;
border: 1px solid rgba(0, 0, 0, 0.4);
font-family: 'Open Sans', sans-serif;
}
 
#menu a {
font-size: 13px;
color: #404040;
display: block;
margin: 0;
padding: 0;
padding: 10px;
text-decoration: none;
border-bottom: 1px solid rgba(0, 0, 0, 0.25);
text-align: center;
}
 
#menu a:last-child {
border: none;
}
 
#menu a:hover {
background-color: #f8f8f8;
color: #404040;
}
 
#menu a.active {
background-color: #3887be;
color: #ffffff;
}
 
#menu a.active:hover {
background: #3074a4;
}
</style>
 
<nav id="menu"></nav>
<div id="map"></div>
<script>
	mapboxgl.accessToken = 'pk.eyJ1IjoiZm91bmRyeXNwYXRpYWwiLCJhIjoiNzk1YTU3OTZmMjZiMzQ3YzM5YzIwODNiNjhkM2MzMDQifQ.sfy6Aux5O-BBqbSVNaec1A';
    	const map = new mapboxgl.Map({
        container: 'map', // container ID
        style: 'mapbox://styles/foundryspatial/ckuenzzg50t8818mssrdk8jol', // style URL
        center: [-116, 49.5], // starting position [lng, lat]
        zoom: 8.01, // starting zoom
	minZoom: 8,
	maxZoom: 15
    });
// After the last frame rendered before the map enters an "idle" state.
map.on('idle', () => {
// If these layers were not added to the map, abort
if (!map.getLayer('rm-01') || !map.getLayer('rm-02') || !map.getLayer('rm-03') || !map.getLayer('rm-04') || !map.getLayer('rm-05') || !map.getLayer('rm-06') || !map.getLayer('rm-07') || !map.getLayer('rm-08') || !map.getLayer('rm-09') || !map.getLayer('rm-10') || !map.getLayer('rm-11') || !map.getLayer('rm-12')) {
return;
}
 
// Enumerate ids of the layers.
const toggleableLayerIds = ['rm-01', 'rm-02', 'rm-03', 'rm-04', 'rm-05', 'rm-06', 'rm-07', 'rm-08', 'rm-09', 'rm-10', 'rm-11', 'rm-12'];
 
// Set up the corresponding toggle button for each layer.
for (const id of toggleableLayerIds) {
// Skip layers that already have a button set up.
if (document.getElementById(id)) {
continue;
}
 
// Create a link.
const link = document.createElement('a');
link.id = id;
link.href = '#';
link.textContent = id;
link.className = '';
 
// Show or hide layer when the toggle is clicked.
link.onclick = function (e) {
const clickedLayer = this.textContent;
e.preventDefault();
e.stopPropagation();
 
const visibility = map.getLayoutProperty(
clickedLayer,
'visibility'
);
 
// Toggle layer visibility by changing the layout object's visibility property.
if (visibility === 'visible') {
map.setLayoutProperty(clickedLayer, 'visibility', 'none');
this.className = '';
} else {
this.className = 'active';
map.setLayoutProperty(
clickedLayer,
'visibility',
'visible'
);
}
};
 
const layers = document.getElementById('menu');
layers.appendChild(link);
}
});
</script>

</body>
</html>
