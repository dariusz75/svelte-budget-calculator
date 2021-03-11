<script>
  import Title from './Title.svelte';
  import Expense from './Expense.svelte';
  import { fly } from 'svelte/transition';
  import { flip } from 'svelte/animate';
  //props
  export let expenses = [];
</script>

<section>
  <Title title="expenses list" />
  <ul>
    {#each expenses as expense, index (expense.id)}
      <div transition:fly={{ x: 200 }} animate:flip>
        <Expense {...expense} />
      </div>
    {:else}
      <h2>currently you have no expenses</h2>
    {/each}
  </ul>
</section>

<style>
  h2 {
    text-transform: capitalize;
  }
</style>
