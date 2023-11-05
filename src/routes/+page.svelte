<Snow />

<main>
  <h1>{import.meta.env.VITE_APP_TITLE}</h1>

  <Calendar />
</main>

<svelte:head>
  <title>{import.meta.env.VITE_APP_TITLE}</title>
</svelte:head>

<script>
  import Calendar from './Calendar.svelte';
  import Snow from './Snow.svelte';
</script>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    color: #fff;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
