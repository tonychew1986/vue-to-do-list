<template>
  <div class="home">
		<section class="todoapp">
			<header class="header">
				<h1>todos</h1>
				<input class="new-todo" v-model="newTodo" v-on:keyup.enter="addTodo" placeholder="What needs to be done?" autofocus>
			</header>
			<section class="main">
				<input id="toggle-all" class="toggle-all" type="checkbox">
				<label for="toggle-all">Mark all as complete</label>
				<ul class="todo-list">
    			<li class="todo" v-for="todo in todos">
    				<div class="view">
    					<input class="toggle" type="checkbox" v-model="todo.completed" />
    					<label>{{ todo.title }}</label>
    					<button class="destroy" @click="removeTodo(todos)"></button>
    				</div>
    				<!-- <input class="edit" value="{{title}}"> -->
    			</li>
        </ul>
        <input class="toggle-all" id="toggle-all" type="checkbox">
        <label for="toggle-all">Mark all as complete</label>
        <ul class="todo-list"></ul>
			</section>
			<footer class="footer"></footer>
		</section>
		<footer class="info">
			<p>Double-click to edit a todo</p>
			<p>Created by <a href="http://sindresorhus.com">Sindre Sorhus</a></p>
			<p>Edited by Tony Chew</p>
			<p>Part of <a href="http://todomvc.com">TodoMVC</a></p>
		</footer>
    <!-- <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from "@/components/HelloWorld.vue";

export default {
  name: "home",
  // components: {
  //   HelloWorld
  // },
  data() {
    return {
      newTodo: "",
      todos: [{ id: 0, title: "New Todo", completed: "false" }]
    };
  },
  methods: {
    addTodo() {
      this.todos.push({
        title: this.newTodo,
        completed: "false",
        id: this.todos.length
      });
    },
    removeTodo(todo) {
      this.todos.splice(this.todos.indexOf(todo), 1)
    }
  }
};
</script>
