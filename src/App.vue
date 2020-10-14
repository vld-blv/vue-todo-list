<template>
  <div id="app">
    <h1>Todo list</h1>
    <AddTodo
      v-on:add-todo="AddTodo"
    />
    <hr>
    <TodoList
      v-bind:todos="todos"
      v-on:remove-todo="removeTodo"
    />
  </div>
</template>

<script>
import TodoList from '@/components/TodoList.vue';
import AddTodo from '@/components/AddTodo.vue';

export default {
  name: 'App',
  data() {
    return {
      todos: [
        { id: 1, title: 'Выучить Vue', completed: false },
        { id: 2, title: 'Устроиться разработчиком', completed: false },
        { id: 3, title: 'Profit', completed: false },
      ],
    };
  },
  components: {
    TodoList,
    AddTodo,
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

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
