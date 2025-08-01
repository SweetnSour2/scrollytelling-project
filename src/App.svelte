<script>
  import { onMount } from 'svelte';
  import ScrollObserver from './lib/ScrollObserver.svelte';
  import BarChart from './lib/BarChart.svelte';
  import LineChart from './lib/LineChart.svelte';
  import { fade } from 'svelte/transition';

  let barData = [];
  let lineData = [];
  let activeStep = 0;

  onMount(async () => {
    const response = await fetch('/data/employer_firms_by_race.json');
    const json = await response.json();

    barData = json.barData;
    lineData = json.lineData;
  });

  function onStepEnter(id) {
    activeStep = id;
  }
</script>

<style>
  main {
    display: flex;
    flex-direction: row;
    height: 100vh;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    color: #222;
  }

  .text-container {
    width: 45%;
    overflow-y: auto;
    padding: 3rem 2rem;
    box-sizing: border-box;
    background: #fff;
  }

  .sticky-chart {
    position: sticky;
    top: 0;
    height: 100vh;
    width: 55%;
    background: #fafafa;
    padding: 3rem 2rem;
    box-sizing: border-box;
    display: flex;
    align-items: center;
    justify-content: center;
    box-shadow: inset -5px 0 5px -5px rgba(0,0,0,0.1);
  }

  section {
    margin-bottom: 6rem;
    min-height: 70vh;
  }

  h1 {
    font-size: 2.4rem;
    margin-bottom: 1rem;
    color: #333;
  }

  h2 {
    font-size: 1.8rem;
    margin-bottom: 1rem;
    color: #444;
  }

  p {
    font-size: 1.1rem;
    line-height: 1.5;
    color: #555;
    max-width: 600px;
  }
</style>

<main>
  <div class="text-container">
    <ScrollObserver id={0} onEnter={onStepEnter}>
      <section in:fade={{ duration: 500 }}>
        <h1>Business Ownership and Racial Wealth Equity</h1>
        <p>
          Business ownership is a fundamental driver of wealth and economic opportunity in the United States.
          However, the number of employer firms varies significantly across racial and ethnic groups, contributing
          to the racial wealth gap.
        </p>
      </section>
    </ScrollObserver>

    <ScrollObserver id={1} onEnter={onStepEnter}>
      <section in:fade={{ duration: 500 }}>
        <h2>Number of Employer Firms by Race/Ethnicity</h2>
        <p>
          This chart shows the total number of employer firms owned by different racial and ethnic groups.
          The disparities highlight systemic barriers that limit wealth building in minority communities.
        </p>
      </section>
    </ScrollObserver>

    <ScrollObserver id={2} onEnter={onStepEnter}>
      <section in:fade={{ duration: 500 }}>
        <h2>Trends Over 2023</h2>
        <p>
          This bar chart would clearly show that, among the listed regions, Georgia had the highest number of Black employer firms in 2023, significantly more than the other states/regions shown.
        </p>
      </section>
    </ScrollObserver>

    <ScrollObserver id={3} onEnter={onStepEnter}>
      <section in:fade={{ duration: 500 }}>
        <h2>Understanding and Addressing Disparities</h2>
        <p>
          Addressing these disparities in business ownership is crucial to closing the racial wealth gap.
          Policies that support minority entrepreneurs can foster a more equitable economy.
        </p>
      </section>
    </ScrollObserver>
  </div>

  <div class="sticky-chart">
    {#if activeStep === 1}
      <BarChart src="C:\Users\norah\code\scrollytelling\static\images/emp.png" alt="Number of Employer Firms by Race/Ethnicity" />
    {:else if activeStep === 2}
      <LineChart src="C:\Users\norah\code\scrollytelling\static\images/chart.png" alt="Number of Employer Firms by Race/Ethnicity" />
    {:else}
      <p style="font-size: 1.3rem; color: #888;">Scroll through the story to explore the data.</p>
    {/if}
  </div>
</main>
