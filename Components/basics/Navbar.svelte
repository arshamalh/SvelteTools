<script>
  export let nav_items = [];
  export let base_href = "";
  export let menu_selected = 1;
</script>

<ul>
  {#each nav_items as item}
    <li>
      <a
        href={base_href}
        on:click|preventDefault={() => (menu_selected = item.value)}
        class:active={menu_selected === item.value}>{item.title}</a
      >
    </li>
  {/each}
</ul>

<style>
  ul {
    display: flex;
    gap: 10px;
    background-color: #333;
    flex-wrap: wrap;
    margin-top: 0;
  }
  ul li {
    display: inline;
    padding: 15px;
  }

  ul li a {
    color: #fff;
  }

  a:hover {
    text-decoration: none;
  }

  .active {
    color: rgb(255, 133, 34);
    font-weight: bolder;
  }
</style>
