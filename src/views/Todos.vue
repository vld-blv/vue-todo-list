<template>
  <div >
    <h2>Todo list</h2>
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
      todos: [],
    };
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
      .then((response) => response.json())
      .then((json) => {
        this.todos = json;
      });
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
