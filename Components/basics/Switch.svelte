<script>
  export let value = "usernames";

  let checked = true;

  function handleClick(event) {
    const target = event.target;
    const state = target.getAttribute("aria-checked");
    checked = state === "true" ? false : true;
    value = checked === true ? "usernames" : "ids";
  }
</script>

<div class="s s--inner">
  <button role="switch" aria-checked={checked} on:click={handleClick}>
    <span>Usernames</span>
    <span>IDs</span>
  </button>
</div>

<style>
  .s--inner {
    margin-top: 10px;
  }

  .s--inner button {
    background-color: #fff;
    padding: 1em;
    border: none;
    outline: none;
  }

  [role="switch"][aria-checked="true"] :first-child,
  [role="switch"][aria-checked="false"] :last-child {
    display: none;
    color: #fff;
  }

  .s--inner button span {
    user-select: none;
    pointer-events: none;
    padding: 0.5em;
    font-size: 18px;
  }

  [role="switch"][aria-checked="true"] :first-child,
  [role="switch"][aria-checked="false"] :last-child {
    border-radius: 0.25em;
    background: darkslateblue;
    display: inline-block;
    transition: 0.5s;
  }
</style>
