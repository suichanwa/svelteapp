<script>
    /**
     * @type {any[]}
     */
    let tasks = [];

    function addTask() {
        tasks = [...tasks, { id: tasks.length, text: `Task ${tasks.length}` }];

        console.log(tasks);
    }

    /**
     * @param {any} id
     */
    function deleteTask(id) {
        tasks = tasks.filter(task => task.id !== id);
    }
</script>

<main>
  <h1 class='todo'>Todo</h1>
  <button on:click={addTask}>Add task</button>

  <ul>
    {#each tasks as task}
      <li>
          {task.text}
          <input type="checkbox">
            <label for="checkbox">Done</label>
          <button on:click={() => deleteTask(task.id)}>Delete</button>
      </li>
    {/each}
  </ul>
</main>

<style>
    .todo {
        font-family: monospace;
        font-size: 2em;
        text-align: center;
        margin-top: 2%;
    }
</style>