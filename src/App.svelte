<script>
  import SingleTodo from "./lib/SingleTodo.svelte";
  import TodoForm from "./lib/TodoForm.svelte";
  let todos = [];
  let disabledState = false;
  const handleAddTodo = (newTodo) => {
    todos = [newTodo, ...todos];
  };
  const handleDeleteTodo = (todoID) => {
    todos = todos.filter((t) => t.id !== todoID);
  };
  const handleCheckTodo = (todoID) => {
    todos = todos.map((t) =>
      t.id === todoID ? { ...t, isComplete: !t.isComplete } : t
    );
  };
  const handleSaveTodo = (todoID, updateTodoName) => {
    todos = todos.map((t) =>
      t.id === todoID ? { ...t, name: updateTodoName } : t
    );
  };
  const handleDisabledState = (newState) => {
    disabledState = newState;
};
</script>

<main>
  <h1>Erciyes University</h1>
  <h2>Master Project</h2>
  <h3>Todo App With Svelte</h3>
  <TodoForm {todos} {handleAddTodo}  {disabledState}/>
  <SingleTodo {todos} {handleDeleteTodo} {handleCheckTodo} {handleSaveTodo} {handleDisabledState} {disabledState}/>
</main>

<style>
  main {
    font-family: "Roboto", sans-serif;
    max-width: 500px;
    min-width: 500px;
  }
  h1,
  h2,
  h3 {
    text-align: center;
  }
</style>
