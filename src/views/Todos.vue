<template>
  <div >
    <h2>Todo list</h2>
    <router-link to="/">Home</router-link>
    <hr>
    <AddTodo
      v-on:add-todo="AddTodo"
    />
    <select v-model="filter">
      <option value="all">All</option>
      <option value="completed">Completed</option>
      <option value="not-completed">Not completed</option>

    </select>
    <hr>
    <Loader v-if="loading" />
    <TodoList
    v-else-if="filteredTodos.length"
      v-bind:todos="filteredTodos"
      v-on:remove-todo="removeTodo"
    />
    <p v-else>No todos. Time to add some!</p>
  </div>
</template>

<script>
import TodoList from '@/components/TodoList.vue';
import AddTodo from '@/components/AddTodo.vue';
import Loader from '@/components/Loader.vue';

export default {
  name: 'App',
  data() {
    return {
      todos: [],
      loading: true,
      filter: 'all',
    };
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
      .then((response) => response.json())
      .then((json) => {
        this.todos = json;
        this.loading = false;
      });
  },
  computed: {
    filteredTodos() {
      if (this.filter === 'completed') {
        return this.todos.filter((el) => el.completed);
      }
      if (this.filter === 'not-completed') {
        return this.todos.filter((el) => !el.completed);
      }

      return this.todos;
    },
  },
  components: {
    TodoList,
    AddTodo,
    Loader,
  },
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter((el) => el.id !== id);
    },
    AddTodo(todo) {
      this.todos.push(todo);
    },
  },
};
</script>
