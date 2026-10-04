
<!DOCTYPE html>
<html lang="bn">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <title>Mahtab Bus Live</title>

  <link rel="stylesheet"
        href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css">

  <style>
    body {
      margin: 0;
      font-family: Arial, sans-serif;
    }

    .header {
      background: #0b57d0;
      color: white;
      text-align: center;
      padding: 14px;
    }

    .header h1 {
      margin: 0;
      font-size: 23px;
    }

    .header p {
      margin: 5px 0 0;
    }

    #map {
      height: 78vh;
      width: 100%;
    }

    .route-info {
      background: white;
      padding: 10px;
      text-align: center;
      font-size: 13px;
    }
  </style>
</head>

<body>

  <div class="header">
    <h1>Mahtab Bus Live</h1>
    <p>🚌 Live Bus Tracking System</p>
  </div>

  <div id="map"></div>

  <div class="route-info">
    লাঙ্গলবন্দ → মালিবাগ → জাঙ্গাল → কেওডালা → মদনপুর
    → চেঙাইন → নাজিমউদ্দিন ভূঁইয়া কলেজ → ললাটি আন্ডারপাস
    → নয়াপুর বাজার → মিরের টেক → বস্তল → গাউসিয়া
    → সাওঘাট → ডহরগাও → ফকির ফ্যাশন
  </div>

  <script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>

  <script>

    const map = L.map('map').setView([23.68, 90.57], 12);

    L.tileLayer(
      'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',
      {
        maxZoom: 19,
        attribution: '&copy; OpenStreetMap contributors'
      }
    ).addTo(map);


    const stops = [
      {name:"লাঙ্গলবন্দ", lat:23.66039, lon:90.56696},
      {name:"মালিবাগ", lat:23.6660, lon:90.5514},
      {name:"জাঙ্গাল", lat:23.6700, lon:90.56951},
      {name:"কেওডালা", lat:23.6750, lon:90.55826},
      {name:"মদনপুর", lat:23.6810, lon:90.54703},
      {name:"চেঙাইন", lat:23.6870, lon:90.5470},
      {name:"নাজিমউদ্দিন ভূঁইয়া কলেজ", lat:23.6920, lon:90.52361},
      {name:"ললাটি আন্ডারপাস", lat:23.6970, lon:90.5471},
      {name:"নয়াপুর বাজার", lat:23.7020, lon:90.598434},
      {name:"মিরের টেক", lat:23.7070, lon:90.5524},
      {name:"বস্তল", lat:23.7120, lon:90.56565},
      {name:"গাউসিয়া", lat:23.7170, lon:90.5653},
      {name:"সাওঘাট", lat:23.7220, lon:90.55917},
      {name:"ডহরগাও", lat:23.7270, lon:90.5604},
      {name:"ফকির ফ্যাশন", lat:23.7320, lon:90.60058}
    ];


    stops.forEach((stop, index) => {

      L.marker([stop.lat, stop.lon])
        .addTo(map)
        .bindPopup(
          "<b>বাস স্টপ " + (index + 1) +
          "</b><br>" + stop.name
        );

    });


    const coordinates = stops
      .map(stop => stop.lon + "," + stop.lat)
      .join(";");


    const url =
      "https://router.project-osrm.org/route/v1/driving/" +
      coordinates +
      "?overview=full&geometries=geojson";


    fetch(url)
      .then(response => response.json())
      .then(data => {

        if (data.code !== "Ok") {
          console.log("Route error:", data);
          return;
        }

        const route = data.routes[0];

        L.geoJSON(route.geometry, {
          style: {
            color: "blue",
            weight: 6
          }
        }).addTo(map);


        map.fitBounds(
          L.geoJSON(route.geometry).getBounds(),
          {
            padding: [20, 20]
          }
        );

      })
      .catch(error => {
        console.log("Routing error:", error);
      });

  </script>

</body>
</html>
