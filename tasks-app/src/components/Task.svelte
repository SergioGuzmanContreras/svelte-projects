<script>
    import { each } from "svelte/internal";

    let tasks = [];
    let taskName = '';

    function addTask(event){
        if(event.key === 'Enter'){
            const task = {
                name: taskName,
                status: false
            }
            tasks.push(task);
            tasks = tasks;
            taskName = '';
        }    
    }

    function deleteTask(index){
        tasks.splice(index, 1);
        tasks = tasks;
    }

    function updateTask(task, index){
        tasks[index].status = !task.status;
    }

</script>

<div>
    <div class="container mt-3">
        <div class="row">
            <div class="col-lg-8 offset-lg-2">
                <input 
                    type="text" 
                    class="form-control form-control-lg" 
                    on:keydown={addTask}
                    bind:value={taskName}
                    placeholder="Enter task...">
                <br>
            </div>
            <div class="col-lg-6 offset-lg-3">
                {#if tasks.length === 0}
                    <div class="card p-2">
                        <h6>There are no tasks to display</h6>
                    </div>
                {/if}

                <ul class="list-group">
                    {#each tasks as task, i}
                        <li class="list-group-item p-1 m-1 d-flex justify-content-between">
                            <!-- svelte-ignore a11y-click-events-have-key-events -->
                            <span class="cursor" on:click={() => updateTask(task, i)}>
                                <i class={task.status ? 'fas fa-check-circle text-success': 'far fa-circle text-primary' }></i>
                            </span>
                            <h5>{task.name}</h5>
                            <!-- svelte-ignore a11y-click-events-have-key-events -->
                            <span class="cursor text-danger" on:click={() => deleteTask(i)}>
                                <i class="fas fa-trash-alt"></i>
                            </span>
                        </li>
                    {/each}
                </ul>
            </div>
        </div>
    </div>
</div>

<style>
    .form-control-lg{
        font-size: 1.8rem;
    }

    input{
        text-align: center;
    }

    .cursor{
        cursor: pointer;
    }

</style>