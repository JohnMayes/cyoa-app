<script>
  import Save from './helpers/Save.svelte';
  import initial_state from './initial_state.js';

  export let Link, state, current_page_name;
</script>

<header>
  <h1>Treasures of the Cursed Pyramid</h1>
</header>

<div class="container">
  <div class="sidebar">
    <p>Dexterity: {$state.stats.dex}</p>
    <p>Strength: {$state.stats.str}</p>
    <span>Charm: {$state.stats.cha}</span>
    <span>Rations: {$state.stats.rat}</span>
  </div>
  <div class="section">
    <slot />
  </div>

  <footer>
    {#if $current_page_name === `Inventory`}
      <span class="currently_on">Inventory</span>
    {:else}
      <Link to="Inventory">Inventory</Link>
    {/if}

    <Save {Link} {state} {current_page_name} />

    <Link to="Start" state={initial_state}>Reset</Link>
  </footer>
</div>

<style>
  .container {
    display: flex;
    flex-direction: row;
  }

  .section {
    display: flex;
    flex-direction: column;
    gap: 16px;
    justify-content: space-between;
    overflow: hidden;

    max-width: 800px;
    margin-left: auto;
    margin-right: auto;
    padding: 16px;

    white-space: normal;

    --blue: #3939ff;
    --green: #00a800;
    --gray: #939393;
  }

  .sidebar {
    display: flex;
    flex-direction: column;
    position: fixed;
    left: 0;
    top: 0;
    height: 100vh;
    width: 15vw;
    background-color: #939393;
    margin-right: 10vw;
  }

  footer {
    padding-top: 16px;

    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  h1 {
    margin: 2rem;
    text-align: center;
  }

  .currently_on {
    font-weight: 700;
  }

  .container :global(p),
  .container :global(button),
  .container :global(a) {
    font-size: 16px;
  }

  .container :global(hr) {
    color: var(--gray);
  }
</style>
