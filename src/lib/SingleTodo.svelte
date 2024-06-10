<script>
  export let todos;
  export let handleDeleteTodo;
  export let handleCheckTodo;
  export let handleSaveTodo;
  
  export let disabledState;
  export let handleDisabledState;

  let updateTodoName;
  const deleteTodo = (todoId) => {
    todos = todos.filter((t) => t.id !== todoId);
    handleDeleteTodo(todoId);
  };

  const checkTodo = (todoId) => {
    todos = todos.map((t) =>
      t.id === todoId ? { ...t, isComplete: !t.isComplete } : t
    );
    handleCheckTodo(todoId);
  };
  
  const editTodo = (todoID) => {
    todos = todos.map((t) =>
      t.id === todoID ? { ...t, isEdit: !t.isEdit } : t
    );
    handleDisabledState(!disabledState)
    updateTodoName = todos.find((t) => t.id === todoID).name;
  };

  const saveTodo = (todoID) => {
    todos = todos.map((t) =>
      t.id === todoID ? { ...t, isEdit: !t.isEdit } : t
    );
    handleSaveTodo(todoID, updateTodoName);
    handleDisabledState(!disabledState)
    updateTodoName = "";
  };
</script>

<div>
  {#each todos as todo}
    <div>
      {#if todo.isEdit}
        <form
          on:submit|preventDefault={() => saveTodo(todo.id)}
          class="edit-form"
        >
          <input
            type="text"
            bind:value={updateTodoName}
            placeholder="Please update your todo!"
          />
          <button type="submit">
            <i class="fa-solid fa-floppy-disk fa-xl icon"></i>
          </button>
        </form>
      {:else}
        <div class="todo-container" class:active={todo.isComplete}>
          <p class="todo-name" class:done={todo.isComplete}>{todo.name}</p>
          <div class="todo-buttons">
            <button
              class="todo-button"
              on:click={() => deleteTodo(todo.id)}
              aria-label="delete todo"
            >
              <i class="fa-solid fa-trash-can fa-xl"></i>
            </button>
            <button
              class="todo-button"
              disabled={disabledState}
              on:click={() => editTodo(todo.id)}
              aria-label="edit todo"
            >
              <i class="fa-solid fa-pen fa-xl"></i>
            </button>
            <button
              class="todo-button"
              class:tick={todo.isComplete}
              on:click={() => checkTodo(todo.id)}
              aria-label="check todo"
            >
              <i class="fa-solid fa-circle-check fa-xl"></i>
            </button>
          </div>
        </div>
      {/if}
    </div>
  {/each}
</div>

<style>
  form {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100%;
    border-radius: 10px;
    box-shadow: 0px 0px 5px 0px rgba(128, 128, 128, 1);
    -webkit-box-shadow: 0px 0px 5px 0px rgba(128, 128, 128, 1);
    -moz-box-shadow: 0px 0px 5px 0px rgba(128, 128, 128, 1);
  }
  .edit-form {
    margin: 50px 0;
  }
  input {
    padding: 15px;
    width: 100%;
    border-radius: 10px 0 0 10px;
    border: 1px solid gray;
    border-right: none;
    color: gray;
    outline: none;
    font-size: 16px;
    font-weight: bold;
    transition: 0.3s ease;
  }
  input:focus {
    border-color: darkblue;
    color: darkblue;
    box-shadow: 0px 0px 15px 0px darkblue;
    -webkit-box-shadow: 0px 0px 15px 0px darkblue;
    -moz-box-shadow: 0px 0px 15px 0px darkblue;
  }
  button {
    background-color: darkblue;
    color: white;
    outline: none;
    border: 1px solid darkblue;
    border-radius: 0px 10px 10px 0;
    padding: 15px;
    font-size: 16px;
    font-weight: bold;
    transition: 0.3s ease;
    cursor: pointer;
  }
  .icon:hover {
    animation: rotation 2s linear infinite;
  }

  @keyframes rotation {
    from {
      transform: rotateY(0deg);
    }
    to {
      transform: rotateY(360deg);
    }
  }

  .todo-container {
    width: inherit;
    display: flex;
    justify-content: space-between;
    align-items: center;
    border-radius: 10px;
    padding: 10px;
    margin: 20px 0;
    border: 2px solid gray;
    border-left: 10px solid gray;
    transition: 0.3s ease;
  }
  .todo-name {
    color: gray;
    font-size: 20px;
    font-weight: bold;
    text-transform: capitalize;
    transition: 0.3s ease;
    margin-left: 20px;
  }
  .active {
    border: 2px solid darkblue;
    border-left: 10px solid darkblue;
  }
  .done {
    color: darkblue;
  }
  .todo-buttons {
    display: flex;
    align-items: center;
    gap: 10px;
  }
  .todo-button {
    padding: 10px;
    border: none;
    background-color: transparent;
    border-radius: 10px;
    cursor: pointer;
    transition: 0.3s ease;
    color: gray;
  }
  .todo-button:hover {
    background-color: darkblue;
    color: white;
  }
  .tick {
    color: green;
  }
  .disable {
    color: gray;
  }
  .disable:hover {
    color: gray;
    background-color: none;
  }

  @media (max-width: 768px) {
    .todo-buttons {
      flex-direction: column;
    }
  }
</style>
