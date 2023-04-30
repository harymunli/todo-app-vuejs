<template>
  <div id="app">
    <h1>To-Do App</h1>
    <form @submit.prevent="addTodo">
      <label>New To-Do</label>
      <input v-model="new_todo" name="new_todo">
      <button>Add To-Do</button>
    </form>
    <h2>To-Do List</h2>
    <ul>
      <li v-for="(todo, index) in todos" 
        :key="index">
      <span :class="{done: todo.done}"
        @click="todo.done = !todo.done"
        >{{todo.content}}</span>
      <button @click="removeTodo(index)">Remove</button>
      </li>
    </ul>
    <h4 v-if="todos.length === 0" >Empty list.</h4>
  </div>
</template>

<script>
export default {
  data(){
    return {
      new_todo : '',
      todos : [
        {
          done: false,
          content: 'Learn HTML'
        },
        {
          done: false,
          content: 'Learn Javascript'
        },
        {
          done: false,
          content: 'Learn Vue'
        }
      ]        
    }
  },
  methods: {
    removeTodo(index) {
      this.todos.splice(index, 1);
    },
    addTodo(){
      this.todos.push({ done: false, content: this.new_todo});
    },
  }
}
</script>
<style>
.done {
  text-decoration: line-through;
}
</style>