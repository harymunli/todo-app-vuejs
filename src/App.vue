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
    <h4 v-if="todos.length === 0">Empty list.</h4>
  </div>
</template>

<script>
export default {
  data(){
    return {
      new_todo : '',
      defaultData : [
        {
          done: true, content: 'Learn HTML'
        },
        {
          done: false, content: 'Learn Vue'
        },
        {
          done: false, content: 'Have fun'
        }
      ],
      lsData : JSON.parse(localStorage.getItem('todos'))     
    }
  },

  computed: {
    todos() {
      return this.defaultData.length === 0 
        ? this.lsData
        : this.defaultData 
    }
  },
  methods: {
    saveData(){
      const storageData = JSON.stringify(this.todos);
      localStorage.setItem('todos', storageData);
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
      this.saveData();
    },
    addTodo(){
      this.todos.push({ done: false, content: this.new_todo});
      this.saveData()
    }
  }
}
</script>
<style lang="scss">
$border: 2px solid
	rgba(
		$color: white,
		$alpha: 0.35,
	);
$size1: 6px;
$size2: 12px;
$size3: 18px;
$size4: 24px;
$size5: 48px;
$backgroundColor: #27292d;
$textColor: white;
$primaryColor: #a0a4d9;
$secondTextColor: #1f2023;
body {
	margin: 0;
	padding: 0;
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	background-color: $backgroundColor;
	color: $textColor;
	#app {
		max-width: 600px;
		margin-left: auto;
		margin-right: auto;
		padding: 20px;
		h1 {
			font-weight: bold;
			font-size: 28px;
			text-align: center;
		}
		form {
			display: flex;
			flex-direction: column;
			width: 100%;
			label {
				font-size: 14px;
				font-weight: bold;
			}
			input,
			button {
				height: $size5;
				box-shadow: none;
				outline: none;
				padding-left: $size2;
				padding-right: $size2;
				border-radius: $size1;
				font-size: 18px;
				margin-top: $size1;
				margin-bottom: $size2;
			}
			input {
				background-color: transparent;
				border: $border;
				color: inherit;
			}
		}
		button {
			cursor: pointer;
			background-color: $primaryColor;
			border: 1px solid $primaryColor;
			color: $secondTextColor;
			font-weight: bold;
			outline: none;
			border-radius: $size1;
		}
		h2 {
			font-size: 22px;
			border-bottom: $border;
			padding-bottom: $size1;
		}
		ul {
			padding: 10px;
			li {
				display: flex;
				justify-content: space-between;
				align-items: center;
				border: $border;
				padding: $size2 $size4;
				border-radius: $size1;
				margin-bottom: $size2;
				span {
					cursor: pointer;
				}
				.done {
					text-decoration: line-through;
				}
				button {
					font-size: $size2;
					padding: $size1;
				}
			}
		}
		h4 {
			text-align: center;
			opacity: 0.5;
			margin: 0;
		}
	}
}
</style>