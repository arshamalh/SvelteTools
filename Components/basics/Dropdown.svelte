<script>
  import Select from "svelte-select";
  import { createEventDispatcher } from "svelte";
  import { copyToClipboard } from "./copyToClipboard";

  export let items = [];

  const dispatch = createEventDispatcher();

  let item = undefined;

  function handleSelect(event) {
    item = event.detail;
    dispatch("change-account", event.detail);
  }

  function handleClear() {
    item = undefined;
    dispatch("clear-account", undefined);
  }
</script>

<div>
  <form>
    <label for="account">Active Account:</label>
    <Select
      id="account"
      {items}
      on:select={handleSelect}
      on:clear={handleClear}
    />
  </form>

  {#if item}
    <p>Username: {item.username}</p>
    <button
      on:click={() => {
        copyToClipboard(item.password)
          .then(() => alert("Password copied to clipboard!"))
          .catch(() => alert("Oops, unable to copy!"));
      }}
    >
      Copy Password
    </button>
  {/if}
</div>

<style>
  div {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  form {
    text-align: center;
    width: 250px;
    background: #f4f4f4;
    padding: 20px;
    border-radius: 4px;
  }

  label {
    margin: 0 0 10px;
  }
</style>
