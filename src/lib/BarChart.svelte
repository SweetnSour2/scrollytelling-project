<script>
  import { onMount } from 'svelte';
  import Chart from 'chart.js/auto';
  export let data; // [{group: 'White', value: 50000}, ...]

  let canvas;
  let chart;

  onMount(() => {
    const ctx = canvas.getContext('2d');
    chart = new Chart(ctx, {
      type: 'bar',
      data: {
        labels: data.map(d => d.group),
        datasets: [{
          label: 'Number of Employer Firms',
          data: data.map(d => d.value),
          backgroundColor: [
            '#4caf50',
            '#2196f3',
            '#ff9800',
            '#9c27b0',
            '#f44336'
          ],
          borderRadius: 5,
          barPercentage: 0.6
        }]
      },
      options: {
        responsive: true,
        animation: { duration: 1000 },
        plugins: {
          legend: { display: false }
        },
        scales: {
          y: {
            beginAtZero: true,
            ticks: {
              callback: val => val.toLocaleString()
            },
            title: {
              display: true,
              text: 'Number of Firms'
            }
          },
          x: {
            title: {
              display: true,
              text: 'Race / Ethnicity'
            }
          }
        }
      }
    });
  });


  import { onDestroy } from 'svelte';
  onDestroy(() => {
    chart.destroy();
  });
</script>

