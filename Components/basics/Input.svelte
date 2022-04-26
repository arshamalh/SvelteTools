<script>
    export let value;
    export let placeholder;
  </script>
  
  <input type="text" bind:value {placeholder} />
  
  <style>
    input {
      flex-grow: 2;
      border: 2px solid #aaa;
      padding: 8px 10px;
      border-radius: 8px;
      margin-top: 15px;
      font-size: 16px;
      transition: border 200ms;
    }
  
    input:focus {
      outline: none;
      border: 2px solid rebeccapurple;
    }
  </style>
  