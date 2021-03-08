<script>
  import Navbar from './components/Navbar.svelte';
  import ExpensesList from './components/ExpensesList.svelte';

  import expensesData from './expenses';

  let expenses = [...expensesData];
</script>

<Navbar />

<main class="content"><ExpensesList {expenses} /></main>
