<script>
  export let value;
  export let placeholder;
  export let cols = "30";
  export let rows = "20";
</script>

<textarea {placeholder} bind:value {cols} {rows} />

<style>
  textarea {
    border: 2px solid #aaa;
    padding: 8px 10px;
    border-radius: 8px;
    margin-top: 15px;
    font-size: 16px;
    transition: border 200ms;
  }

  textarea:focus {
    outline: none;
    border: 2px solid rebeccapurple;
  }
</style>
