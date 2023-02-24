<script lang="ts">
    import {browser} from '$app/environment';

    //    get from local storage
    let todos = [];

    if (browser) {
        const todosFromStorage = localStorage.getItem("todos");
        if (todosFromStorage) {
            todos = JSON.parse(todosFromStorage);
        }
    }
    let newTodo = "";

    const addTodo = () => {
        if (!newTodo) return;

        todos = [...todos, {text: newTodo, done: false}];
        newTodo = "";
        //    save to local storage
        localStorage.setItem("todos", JSON.stringify(todos));
    }

    const toggleTodo = (index) => {

        todos[index].done = !todos[index].done;


        localStorage.setItem("todos", JSON.stringify(todos));
        localStorage.setItem("todos", JSON.stringify(todos));
    }

    const getRandom = () => {

        // range 1 - 180
        return Math.floor(Math.random() * 360) + 1;
    }

</script>

<div class="todos">

    <input type="text" bind:value={newTodo}>

    <button on:click={addTodo}>Add</button>

    {#each todos as todo, index}
        <div class="todo"><span style={`--hue: ${getRandom()}deg`}>{index + 1}.</span> {todo.text}<input type=checkbox bind:checked={todo.done}
                                                                                 on:click={() => toggleTodo(index)}></div>
    {/each}
</div>

<style lang="scss">
  .todos {
    display: flex;
    flex-direction: column;
    align-items: center;

    input[type=text] {
      width: 300px;
      height: 30px;
      font-size: 20px;
      margin: 10px 0;
    }

    button {
      width: 300px;
      height: 30px;
      font-size: 20px;
      margin: 10px 0;
    }

    & .todo {
      width: 300px;
      height: 30px;
      font-size: 20px;
      margin: 10px 0;

      display: flex;
      align-items: center;
      justify-content: space-between;

      span {

        color: hsl(var(--hue), 100%, 50%);
      }

    }

    & .todo input[type=checkbox] {
      margin-left: 10px;
      height: 30px;
      width: 20px;
      cursor: pointer;

    }


  }

</style>
