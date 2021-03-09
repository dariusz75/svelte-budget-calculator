<script>
  import { setContext } from 'svelte';
  //components
  import Navbar from './components/Navbar.svelte';
  import ExpensesList from './components/ExpensesList.svelte';
  import Totals from './components/Totals.svelte';
  //data
  import expensesData from './expenses';
  //variables
  let expenses = [...expensesData];
  //reactive
  $: total = expenses.reduce((accumulator, current) => {
    return (accumulator = accumulator + current.amount);
  }, 0);
  //functions
  const removeExpense = (id) => {
    expenses = expenses.filter((expense) => expense.id !== id);
  };
  const clearExpenses = () => {
    expenses = [];
  };
  //context
  setContext('remove', removeExpense);
</script>

<Navbar />

<main class="content">
  <Totals title="total exppenses" {total} />
  <ExpensesList {expenses} />
  <button
    type="button"
    class="btn btn-primary btn-block"
    on:click={clearExpenses}>clear expenses</button
  >
</main>
