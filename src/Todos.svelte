<script>
  import TodoItem from "./TodoItem.svelte";

  let newTodoTitle = "";
  let currentFilter = "all";
  let nextId = 4;

  let todos = [
    {
      id: 1,
      title: "My first todo",
      completed: false,
    },
    {
      id: 2,
      title: "My second todo",
      completed: false,
    },
    {
      id: 3,
      title: "My third todo",
      completed: false,
    },
  ];

  function addTodoItem(event) {
    if (event.key === "Enter") {
      todos = [
        ...todos,
        {
          id: nextId,
          completed: false,
          title: newTodoTitle,
        },
      ];

      nextId++;
      newTodoTitle = "";
    }
  }

  function handleDeleteTodo(event) {
    todos = todos.filter((todo_item) => {
      return todo_item.id !== event.detail.id;
    });
  }

  function handleCompleteTodo(event) {
    const idx = todos.findIndex(
      (todo_item) => todo_item.id === event.detail.id
    );
    console.log(todos);
    todos[idx].completed = event.detail.completed;
    console.log(todos);
  }
</script>

<div class="container">
  <h2>Just a to-do list</h2>
  <input
    type="text"
    name="new-todo-item"
    class="todo-input"
    placeholder="Got a new task? Feed it to me..."
    bind:value={newTodoTitle}
    on:keydown={addTodoItem} />

  {#each todos as todo}
    <div class="todo-item">
      <TodoItem
        {...todo}
        on:deleteTodo={handleDeleteTodo}
        on:toggleComplete={handleCompleteTodo} />
    </div>
  {/each}
</div>
