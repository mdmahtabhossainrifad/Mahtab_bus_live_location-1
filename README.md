<!DOCTYPE html>
<html lang="bn">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Mahtab Bus Live</title>

<style>
html, body {
    margin: 0;
    padding: 0;
    width: 100%;
    height: 100%;
    font-family: Arial, sans-serif;
}

#header {
    height: 65px;
    background: #0b57d0;
    color: white;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}

#header h1 {
    margin: 0;
    font-size: 22px;
}

#header p {
    margin: 4px 0 0;
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

<script>

function loadLeaflet() {

    var css = document.createElement("link");

    css.rel = "stylesheet";
    css.href = "https://unpkg.com/leaflet@1.9.4/dist/leaflet.css";

    document.head.appendChild(css);


    var script = document.createElement("script");

    script.src = "https://unpkg.com/leaflet@1.9.4/dist/leaflet.js";

    script.onload = startMap;

    document.body.appendChild(script);
}


function startMap() {

    var map = L.map("map").setView(
        [23.69, 90.56],
        12
    );


    L.tileLayer(
        "https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png",
        {
            maxZoom: 19,
            attribution:
            "&copy; OpenStreetMap contributors"
        }
    ).addTo(map);


    var stops = [

        {
            name: "লাঙ্গলবন্দ",
            lat: 23.66039,
            lon: 90.56696
        },

        {
            name: "মালিবাগ",
            lat: 23.6660,
            lon: 90.5514
        },

        {
            name: "জাঙ্গাল",
            lat: 23.6700,
            lon: 90.56951
        },

        {
            name: "কেওডালা",
            lat: 23.6750,
            lon: 90.55826
        },

        {
            name: "মদনপুর",
            lat: 23.6810,
            lon: 90.54703
        },

        {
            name: "চেঙাইন",
            lat: 23.6870,
            lon: 90.5470
        },

        {
            name: "নাজিমউদ্দিন ভূঁইয়া কলেজ",
            lat: 23.6920,
            lon: 90.52361
        },

        {
            name: "ললাটি আন্ডারপাস",
            lat: 23.6970,
            lon: 90.5471
        },

        {
            name: "নয়াপুর বাজার",
            lat: 23.7020,
            lon: 90.598434
        },

        {
            name: "মিরের টেক",
            lat: 23.7070,
            lon: 90.5524
        },

        {
            name: "বস্তল",
            lat: 23.7120,
            lon: 90.56565
        },

        {
            name: "গাউসিয়া",
            lat: 23.7170,
            lon: 90.5653
        },

        {
            name: "সাওঘাট",
            lat: 23.7220,
            lon: 90.55917
        },

        {
            name: "ডহরগাও",
            lat: 23.7270,
            lon: 90.5604
        },

        {
            name: "ফকির ফ্যাশন",
            lat: 23.7320,
            lon: 90.60058
        }

    ];


    var points = [];


    stops.forEach(function(stop, index) {

        var marker = L.marker([
            stop.lat,
            stop.lon
        ]).addTo(map);


        marker.bindPopup(
            "<b>বাস স্টপ " +
            (index + 1) +
            "</b><br>" +
            stop.name
        );


        points.push([
            stop.lat,
            stop.lon
        ]);

    });


    L.polyline(
        points,
        {
            color: "blue",
            weight: 6
        }
    ).addTo(map);


    map.fitBounds(points, {
        padding: [30, 30]
    });


    var busIcon = L.divIcon({

        html:
        '<div style="' +
        'font-size:32px;' +
        'text-align:center;' +
        '">🚌</div>',

        className: "",

        iconSize: [40, 40],

        iconAnchor: [20, 20]

    });


    var bus = L.marker(
        points[0],
        {
            icon: busIcon
        }
    ).addTo(map);


    bus.bindPopup(
        "<b>Mahtab Bus Live</b><br>" +
        "🚌 বাস বর্তমানে লাঙ্গলবন্দে"
    );

}


loadLeaflet();

</script>

</body>
</html>
