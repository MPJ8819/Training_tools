# Training_tools
<!DOCTYPE html>
<html>
<head>
  <title>Time in Power Zones</title>
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
</head>
<body>
  <h2>Time in Power Zones (2025)</h2>
  <canvas id="zonesChart"></canvas>

  <script>
    async function loadData() {
      const res = await fetch("https://intervals.icu/api/v1/athlete/1870423/activities", {
        headers: { "Authorization": 5ix163s80ie4yd81hr5w6ew42 }
      });
      const activities = await res.json();

      const zones = [0,0,0,0,0,0,0];
      const year = new Date().getFullYear();

      activities.forEach(act => {
        const d = new Date(act.date);
        if (d.getFullYear() === year && act.power_zones) {
          act.power_zones.forEach((z, i) => {
            zones[i] += z;
          });
        }
      });

      const ctx = document.getElementById('zonesChart').getContext('2d');
      new Chart(ctx, {
        type: 'bar',
        data: {
          labels: ['Z1','Z2','Z3','Z4','Z5','Z6','Z7'],
          datasets: [{
            label: 'Seconds in Zone',
            data: zones
          }]
        }
      });
    }

    loadData();
  </script>
</body>
</html>
