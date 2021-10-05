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
<div id="map"></div>
<script>
	mapboxgl.accessToken = 'pk.eyJ1IjoiZm91bmRyeXNwYXRpYWwiLCJhIjoiNzk1YTU3OTZmMjZiMzQ3YzM5YzIwODNiNjhkM2MzMDQifQ.sfy6Aux5O-BBqbSVNaec1A';
    	const map = new mapboxgl.Map({
        container: 'map', // container ID
        style: 'mapbox://styles/mapbox/streets-v11', // style URL
        center: [-115, 53], // starting position [lng, lat]
        zoom: 9 // starting zoom
    });
	map.on('load', () => {
// Add a data source containing GeoJSON data.
map.addSource('risk-levels', {
'type': 'geojson',
'data': 'https://foundryspatial.github.io/kwt-risklevels/risk_levels.geojson'
});
 
// Add a new layer to visualize the lines.
map.addLayer({
'id': 'rl-01',
'type': 'line',
'source': 'risk-levels', // reference the data source
'layout': {
	'line-join': 'round',
	'line-cap': 'round'
	},
'paint': {
'line-color': [
	'match',
	['get', 'rl_01']
	'1',
	'#0080fa', 
	'2',
	'#FFFF00',
	'3',
	'#FF0000'
	]
}
});
});
});
</script>

</body>
</html>
