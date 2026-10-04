<!DOCTYPE html>
<html lang="bn">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Mahtab Bus Live</title>

<link rel="stylesheet"
href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css">

<style>
html, body {
    margin: 0;
    padding: 0;
    width: 100%;
    height: 100%;
}

body {
    font-family: Arial, sans-serif;
}

#header {
    height: 65px;
    background: #0b57d0;
    color: white;
    text-align: center;
    padding-top: 10px;
    box-sizing: border-box;
}

#header h1 {
    margin: 0;
    font-size: 22px;
}

#header p {
    margin: 4px 0;
    font-size: 13px;
}

#map {
    width: 100%;
    height: calc(100vh - 65px);
}
</style>
</head>

<body>

<div id="header">
    <h1>Mahtab Bus Live</h1>
    <p>🚌 Live Bus Tracking System</p>
</div>

<div id="map"></div>

<script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>

<script>

var map = L.map("map").setView([23.69, 90.56], 12);

L.tileLayer(
    "https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png",
    {
        maxZoom: 19,
        attribution: "&copy; OpenStreetMap contributors"
    }
).addTo(map);


var stops = [

    ["লাঙ্গলবন্দ", 23.66039, 90.56696],
    ["মালিবাগ", 23.6660, 90.5514],
    ["জাঙ্গাল", 23.6700, 90.56951],
    ["কেওডালা", 23.6750, 90.55826],
    ["মদনপুর", 23.6810, 90.54703],
    ["চেঙাইন", 23.6870, 90.5470],
    ["নাজিমউদ্দিন ভূঁইয়া কলেজ", 23.6920, 90.52361],
    ["ললাটি আন্ডারপাস", 23.6970, 90.5471],
    ["নয়াপুর বাজার", 23.7020, 90.598434],
    ["মিরের টেক", 23.7070, 90.5524],
    ["বস্তল", 23.7120, 90.56565],
    ["গাউসিয়া", 23.7170, 90.5653],
    ["সাওঘাট", 23.7220, 90.55917],
    ["ডহরগাও", 23.7270, 90.5604],
    ["ফকির ফ্যাশন", 23.7320, 90.60058]

];


var routePoints = [];


stops.forEach(function(stop, index) {

    var lat = stop[1];
    var lon = stop[2];

    var marker = L.marker([lat, lon])
        .addTo(map);

    marker.bindPopup(
        "<b>বাস স্টপ " +
        (index + 1) +
        "</b><br>" +
        stop[0]
    );

    routePoints.push([lat, lon]);

});


L.polyline(
    routePoints,
    {
        color: "blue",
        weight: 6
    }
).addTo(map);


map.fitBounds(routePoints);


var busIcon = L.divIcon({
    html: "🚌",
    className: "bus-icon",
    iconSize: [35, 35],
    iconAnchor: [17, 17]
});


var bus = L.marker(
    routePoints[0],
    {
        icon: busIcon
    }
).addTo(map);


bus.bindPopup(
    "<b>Mahtab Bus Live</b><br>" +
    "🚌 বাস বর্তমানে লাঙ্গলবন্দে"
);

</script>

</body>
</html>
