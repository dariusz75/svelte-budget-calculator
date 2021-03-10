<script>
  //components
  import Title from './Title.svelte';

  //props
  export let name = '';
  export let amount = null;
  export let addExpense;
  export let isEditing;
  export let editExpense;

  //reactive variables
  $: isEmpty = !name || !amount;

  //functions
  const handleSubmit = (e) => {
    e.preventDefault();
    if (isEditing) {
      editExpense({ name, amount });
    } else {
      addExpense({ amount: amount, name: name });
    }
    name = '';
    amount = null;
  };
</script>

<section class="form">
  <Title title="add expense" />
  <form class="expense-form" on:submit={handleSubmit}>
    <div class="form-control">
      <label for="name">name</label>
      <input type="text" id="name" bind:value={name} />
    </div>
    <div class="form-control">
      <label for="amount">amount</label>
      <input type="number" id="amount" bind:value={amount} />
    </div>
    {#if isEmpty}
      <p class="form-empty">please feel out all form fields</p>{/if}

    <button
      type="submit"
      class="btn btn-block"
      class:disabled={isEmpty}
      disabled={isEmpty}
    >
      {#if isEditing}edit expense{:else} add expense{/if}</button
    >
    <button type="button" class="close-btn "
      >close <i class="fas fa-times" />
    </button>
  </form>
</section>
