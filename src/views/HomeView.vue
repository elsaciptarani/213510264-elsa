<template>
	<h1>Jadwal Ujian Tengah Semester </h1>
	<div class="todo-app">
	  <input v-model="newTodo" placeholder="Tambah Mata Kuliah">
	  <button @click="addTodo">Add</button>
	  <br><br>
	  <button @click="hideCompleted = !hideCompleted">{{ hideCompleted ? 'Seluruh Mata Kuliah' : 'Mata Kuliah Belum Selesai' }}</button>
	  <ul>
		<li v-for="todo in visibleTodos" :key="todo.id">
		  <span :class="{ 'completed': todo.completed }" @click="toggleComplete(todo)">{{ todo.text }}</span>
		  <button v-if="!todo.completed" @click="completeTodo(todo.id)">Selesai</button>
		  <button v-if="todo.completed" @click="unCompleteTodo(todo.id)">Belum Selesai</button>
		  <button @click="removeTodo(todo.id)">Hapus</button>
		</li>
	  </ul>
	</div>
  </template>
  
  <script>
  export default {
	name: 'App',
	data() {
	  return {
		todos: [],
		newTodo: '',
		nextId: 1,
		hideCompleted: false
	  }
	},
	computed: {
	  visibleTodos() {
		if (this.hideCompleted) {
		  return this.todos.filter(todo => !todo.completed);
		} else {
		  return this.todos;
		}
	  }
	},
	methods: {
	  addTodo() {
		if (this.newTodo.trim() !== '') {
		  this.todos.push({
			id: this.nextId++,
			text: this.newTodo,
			completed: false
		  });
		  this.newTodo = '';
		}
	  },
	  removeTodo(id) {
		this.todos = this.todos.filter(todo => todo.id !== id);
	  },
	  completeTodo(id) {
		const todo = this.todos.find(todo => todo.id === id);
		if (todo) {
		  todo.completed = true;
		}
	  },
	  unCompleteTodo(id) {
		const todo = this.todos.find(todo => todo.id === id);
		if (todo) {
		  todo.completed = false;
		}
	  },
	  toggleComplete(todo) {
		todo.completed = !todo.completed;
	  }
	}
  }
  </script>
  
  <style>

body {
	background : linear-gradient(135deg, #153677, #380745);
}

h1 {
	color: plum;
  
  align-items: center;
  margin-bottom: 20px;
}

ul li{
  list-style-type: none;
  padding: 12px 8px 12px 50px;
  font-size: 17px;
  user-select: none;
  cursor: pointer;
  margin: 0;
  position: relative;
  color : #153677;
 
}


.completed {
  text-decoration: line-through;
}
button {
  margin-left: 10px;
  border: none;
  outline: none;
  padding: 5px 10px;
  background: #290052;
  color: #fff;
  font-size: 14px;
  cursor: pointer;
  border-radius: 40px;
}

.todo-app{
  width: 100%;
  max-width: 540px;
  background: plum;
  margin: 100px auto 20px;
  padding: 40px 30px 70px;
  border-radius: 10px;
}


</style>