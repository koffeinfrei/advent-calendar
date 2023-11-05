<script>
  import Door from './Door.svelte';
</script>

<div class="calendar">
  {#each { length: 24 } as _, index}
    <Door number={index + 1} />
  {/each}
</div>

<style>
  .calendar {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    margin: auto;
    max-width: 1280px;
  }
</style>
