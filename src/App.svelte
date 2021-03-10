<script>
  import { setContext } from 'svelte';

  //components
  import Navbar from './components/Navbar.svelte';
  import ExpensesList from './components/ExpensesList.svelte';
  import Totals from './components/Totals.svelte';
  import ExpenseForm from './components/ExpenseForm.svelte';

  //data
  import expensesData from './expenses';

  //variables
  let expenses = [...expensesData];

  //set editing variables
  let setId = null;
  let setName = '';
  let setAmount = null;

  //reactive variables
  $: isEditing = setId ? true : false;
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

  const addExpense = ({ name, amount }) => {
    let expense = {
      id: Math.random() * Date.now(),
      name: name,
      amount: amount,
    };
    expenses = [expense, ...expenses];
  };

  const setModifiedExpense = (id) => {
    let expense = expenses.find((expense) => expense.id === id);

    setId = expense.id;
    setName = expense.name;
    setAmount = expense.amount;
  };

  const editExpense = ({ name, amount }) => {
    expenses = expenses.map((expense) => {
      return expense.id === setId
        ? { ...expense, name: name, amount: amount }
        : expense;
    });
    setId = null;
    setAmount = null;
    setName = '';
  };

  //context
  setContext('remove', removeExpense);
  setContext('modify', setModifiedExpense);
</script>

<Navbar />
<main class="content">
  <ExpenseForm
    {addExpense}
    {isEditing}
    {editExpense}
    name={setName}
    amount={setAmount}
    id={setId}
  />
  <Totals title="total exppenses" {total} />
  <ExpensesList {expenses} />
  <button
    type="button"
    class="btn btn-primary btn-block"
    on:click={clearExpenses}>clear expenses</button
  >
</main>
