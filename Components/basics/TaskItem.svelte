<script>
  // {title, kind, url, id}
  import { createEventDispatcher } from "svelte";
  export let task;
  const dispatch = createEventDispatcher();
  const handleDone = (task_id) => {
    dispatch("done-task", task_id);
  };
</script>

<div class="task-item">
  <span>
    {task.title}
  </span>
  <small>{task.kind}</small>
  <a href={task.url} target="_blank">Link</a>
  <button on:click={() => handleDone(task)}>Done</button>
</div>

<style>
  .task-item {
    display: flex;
    gap: 10px;
    align-items: center;
    width: 100%;
    background-color: #bbb;
    padding: 10px;
    margin-top: 10px;
    border-radius: 5px;
    transition: all 200ms ease-in-out;
    border-left: 0px hsl(200, 62%, 46%) solid;
    box-sizing: border-box;
  }

  .task-item:hover {
    border-left-width: 7px;
    background-color: #ccc;
  }

  .task-item span {
    flex-grow: 1;
    text-align: start;
  }

  .task-item a {
    color: #111;
    padding: 5px;
    border-radius: 5px;
    font-size: small;
    background-color: rgb(222, 112, 112);
  }

  .task-item button {
    border: none;
    height: 25px;
    border-radius: 5px;
    background-color: rgb(100, 250, 100);
    box-shadow: none;
    cursor: pointer;
  }

  .task-item small {
    padding: 5px;
    border-radius: 5px;
    background-color: rgb(112, 222, 255);
  }
</style>
