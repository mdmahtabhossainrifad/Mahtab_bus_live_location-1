<script>

const map = L.map('map').setView([23.68, 90.57], 12);

L.tileLayer(
  'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',
  {
    maxZoom: 19,
    attribution: '&copy; OpenStreetMap contributors'
  }
).addTo(map);

</script>


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
