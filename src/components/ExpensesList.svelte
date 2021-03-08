<script>
  import Title from './Title.svelte';
  import Expense from './Expense.svelte';

  export let expenses = [];
</script>

<section>
  <Title title="expenses list" />
  <ul>
    {#each expenses as expense, index}
      <Expense {...expense} />
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
