<!DOCTYPE html>
<html lang="bn">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Mahtab Bus Live</title>
<link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css">

<style>
*{box-sizing:border-box}
html,body{margin:0;padding:0;width:100%;height:100%;font-family:Arial,sans-serif}
body{overflow:hidden}
#header{
  height:70px;background:#0b57d0;color:#fff;
  display:flex;align-items:center;justify-content:space-between;
  padding:8px 14px;box-shadow:0 2px 8px rgba(0,0,0,.25);
  position:relative;z-index:1000
}
.title{font-size:20px;font-weight:700}
.subtitle{font-size:12px;margin-top:4px}
.live{
  background:#fff;color:#0b57d0;border-radius:18px;
  padding:7px 10px;font-weight:bold;font-size:12px
}
#map{width:100%;height:calc(100vh - 70px)}
.bus{
  width:44px;height:44px;border-radius:50%;background:#0b57d0;
  border:3px solid white;display:flex;align-items:center;
  justify-content:center;font-size:24px;
  box-shadow:0 2px 8px rgba(0,0,0,.35)
}
#info{
  position:absolute;z-index:900;left:12px;bottom:82px;
  background:#fff;padding:10px 12px;border-radius:10px;
  box-shadow:0 2px 10px rgba(0,0,0,.25);font-size:12px
}
</style>
</head>

<body>

<div id="header">
  <div>
    <div class="title">🚌 Mahtab Bus Live</div>
    <div class="subtitle">Mahtab Hossain Rifad • Live Bus Tracking System</div>
  </div>
  <div class="live">● LIVE</div>
</div>

<div id="map"></div>
<div id="info">রুট: লাঙ্গলবন্দ → ফকির ফ্যাশন<br>বাস বর্তমানে: লাঙ্গলবন্দ</div>

<script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>
<script>
const stops=[
["লাঙ্গলবন্দ",23.66039,90.56696],
["মালিবাগ",23.6660,90.5514],
["জাঙ্গাল",23.6700,90.56951],
["কেওডালা",23.6750,90.55826],
["মদনপুর",23.6810,90.54703],
["চেঙাইন",23.6870,90.5470],
["নাজিমউদ্দিন ভূঁইয়া কলেজ",23.6920,90.52361],
["ললাটি আন্ডারপাস",23.6970,90.5471],
["নয়াপুর বাজার",23.7020,90.598434],
["মিরের টেক",23.7070,90.5524],
["বস্তল",23.7120,90.56565],
["গাউসিয়া",23.7170,90.5653],
["সাওঘাট",23.7220,90.55917],
["ডহরগাও",23.7270,90.5604],
["ফকির ফ্যাশন",23.7320,90.60058]
];

const map=L.map("map").setView([23.69,90.56],13);

L.tileLayer("https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png",{
maxZoom:19,
attribution:"© OpenStreetMap contributors"
}).addTo(map);

const points=[];

stops.forEach((s,i)=>{
  const p=[s[1],s[2]];
  points.push(p);

  const marker=L.marker(p).addTo(map);
  marker.bindPopup(
    "<b>বাস স্টপ "+(i+1)+"</b><br>"+s[0]+
    "<br><small>Mahtab Bus Live</small>"
  );
});

L.polyline(points,{
color:"#0b57d0",
weight:6,
opacity:.85
}).addTo(map);

const busIcon=L.divIcon({
className:"",
html:'<div class="bus">🚌</div>',
iconSize:[44,44],
iconAnchor:[22,22]
});

const bus=L.marker(points[0],{icon:busIcon}).addTo(map);

bus.bindPopup(
"<b>Mahtab Bus Live</b><br>🚌 বাস বর্তমানে লাঙ্গলবন্দ"
);

map.fitBounds(points,{padding:[25,25]});
</script>

</body>
</html>
