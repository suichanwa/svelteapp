<script>
// @ts-nocheck

    import { Button } from 'flowbite-svelte';
    import { tasks } from '../../store.js';

    let taskId = localStorage.getItem('taskId') || 0;

    function addTask() { 
        let currentTasks = $tasks; 
        currentTasks = [...currentTasks, { id: taskId++, text: `Task ${taskId}` }]; 
        tasks.set(currentTasks);
        localStorage.setItem('taskId', taskId);
    }

    function deleteTask(id) {
        let currentTasks = $tasks;
        currentTasks = currentTasks.filter(task => task.id !== id);
        tasks.set(currentTasks);
    }

    function toggleDone(task) {
        let currentTasks = $tasks;
        let taskIndex = currentTasks.findIndex(t => t.id === task.id);
        if (taskIndex !== -1) {
            currentTasks[taskIndex].done = !currentTasks[taskIndex].done;
            tasks.set(currentTasks);
        }
    }
</script>

<main>
  <h1 class='todo'>Todo</h1>
  <Button checked shadow color="dark" on:click={addTask}>Add Task</Button>
    <ul>
        {#each $tasks as task (task.id)} 
        <!-- svelte-ignore a11y-label-has-associated-control -->
        <li>
            <div>
                <label>{task.text}</label>
            </div>
            <input class="inputclass" type="text"> 
            <div class="buttonsdeleteadd"> 
                <Button color={task.done ? 'green' : 'red'} on:click={() => toggleDone(task)}>{task.done ? 'Done' : 'Not Done'}</Button>
                <Button color="red" outline on:click={() => deleteTask(task.id)}>Delete</Button>
            </div>
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
    padding: 10px; /* Adjust as needed */
}

.inputclass {
    display: flex;
    width: 1200px;
    padding: 10px; /* Adjust as needed */
}

ul {
    list-style: none;
    padding: 10px; /* Adjust as needed */
}

li {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px; /* Adjust as needed */
}

.buttonsdeleteadd {
    display: flex;
    gap: 1rem;
    margin-right: 20px;
    padding: 10px; /* Adjust as needed */
}
</style>