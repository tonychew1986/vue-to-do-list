<template>
  <div class="home">
		<section class="todoapp">
			<header class="header">
				<h1>todos</h1>
				<input class="new-todo" v-model="newTodo" v-on:keyup.enter="addTodo" placeholder="What needs to be done?" autofocus>
			</header>
			<section class="main">
				<ul class="todo-list">
    			<li v-for="todo in filteredTodos" :key="todo.id" :class="{completed: todo.completed, editing: todo == editedTodo}">
    				<div class="view">
    					<input class="toggle" type="checkbox" v-model="todo.completed" />
    					<label @dblclick="editTodo(todo)">{{ todo.title }}</label>
    					<button class="destroy" @click="removeTodo(todos)"></button>
    				</div>
    				<input class="edit" type="text" v-model="todo.title" @blur="doneEdit(todo)" @keyup.enter="doneEdit(todo)">
    			</li>
        </ul>
        <input class="toggle-all" id="toggle-all" type="checkbox">
        <label for="toggle-all">Mark all as complete</label>
        <ul class="todo-list"></ul>
			</section>
			<footer class="footer">
        <ul class="filters">
          <li>
            <a href="#" @click.prevent="visibility='all'" :class="{ selected: visibility == 'all' }">
              All
            </a>
          </li>
          <li>
            <a href="#" @click.prevent="visibility='active'" :class="{ selected: visibility == 'active' }">
              Active
            </a>
          </li>
          <li>
            <a href="#" @click.prevent="visibility='completed'" :class="{ selected: visibility == 'completed' }">
              Completed
            </a>
          </li>
        </ul>
      </footer>
		</section>
  </div>
</template>

<script>
const STORAGE_KEY = "todo-storage";

export default {
  name: "home",
  data() {
    return {
      newTodo: "",
      todos: [],
      editedTodo: null,
      visibility: "all"
    };
  },
  created() {
    this.todos = JSON.parse(localStorage.getItem(STORAGE_KEY) || "[]");
  },
  computed: {
    filteredTodos() {
      if (this.visibility === "all") {
        return this.todos;
      } else if (this.visibility === "active") {
        return this.todos.filter(function(todo) {
          return !todo.completed;
        });
      } else if (this.visibility === "completed") {
        return this.todos.filter(function(todo) {
          return todo.completed;
        });
      }
    }
  },
  methods: {
    addTodo() {
      this.todos.push({
        title: this.newTodo,
        completed: false,
        id: this.todos.length
      });
      this.newTodo = "";
      localStorage.setItem(STORAGE_KEY, JSON.stringify(this.todos));
    },
    removeTodo(todo) {
      this.todos.splice(this.todos.indexOf(todo), 1);
      localStorage.setItem(STORAGE_KEY, JSON.stringify(this.todos));
    },
    editTodo(todo) {
      this.editedTodo = todo;
    },
    doneEdit(todo) {
      if (!this.editedTodo) {
        return;
      }
      this.editedTodo = null;
      todo.title = todo.title.trim();
      if (!todo.title) {
        this.removeTodo(todo);
      }
      localStorage.setItem(STORAGE_KEY, JSON.stringify(this.todos));
    }
  }
};
</script>
