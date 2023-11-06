<Snow />

<main>
  <h1>{import.meta.env.VITE_APP_TITLE}</h1>

  <Calendar />
</main>
<footer>
  Made with ☕️ by <a href="https://www.koffeinfrei.org" target="_blank">Koffeinfrei</a>.
  This is free and open source software. Source code on <a href="https://github.com/koffeinfrei/advent-calendar" target="_blank">GitHub</a>
</footer>

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
    margin: 0 auto 4em auto;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }

  footer {
    font-size: 0.8em;
    text-align: center;
    margin-bottom: 1em;
  }

  h1 {
    color: #fff;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }
</style>
