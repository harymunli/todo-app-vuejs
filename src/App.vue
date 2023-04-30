<template>
  <div id="app">
    <h1>To-Do App</h1>
    <form>
      <label>New To-Do</label>
      <input>
      <button>Add To-Do</button>
    </form>
    <h2>To-Do List</h2>
    <ul>
      <li>
        learn vue
        <button>Remove</button>
      </li>
    </ul>
    <!-- <h4 v-if="todos.length === 0" >Empty list.</h4> -->
    <h4>Empty list.</h4>
  </div>
</template>