<script>
  import { onMount } from 'svelte';
  import Chart from 'chart.js/auto';
  export let data;

  let canvas;
  let chart;

  onMount(() => {
    const ctx = canvas.getContext('2d');

    const labels = data.map(d => d.year);
    const groups = Object.keys(data[0]).filter(k => k !== 'year');
    const colors = ['#4caf50', '#2196f3', '#ff9800', '#9c27b0', '#f44336'];

    const datasets = groups.map((group, i) => ({
      label: group,
      data: data.map(d => d[group]),
      borderColor: colors[i],
      backgroundColor: colors[i] + '55',
      fill: false,
      tension: 0.25,
      pointRadius: 4,
      pointHoverRadius: 6,
      borderWidth: 3
    }));

    chart = new Chart(ctx, {
      type: 'line',
      data: { labels, datasets },
      options: {
        responsive: true,
        plugins: {
          legend: { position: 'bottom' }
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
              text: 'Year'
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

<canvas bind:this={canvas} style="max-width: 100%; height: 400px;"></canvas>
