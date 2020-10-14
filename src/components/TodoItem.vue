<template>
  <li>
    <span v-bind:class="{done: todo.completed}">
      <input type="checkbox" v-on:change="todo.completed = !todo.completed">
      <strong>{{ index + 1 }}</strong>
      {{ todo. title | upperCase }}
    </span>
    <button class="button-remove"
            v-on:click="$emit('remove-todo', todo.id)">&times;</button>
  </li>
</template>

<script>
export default {
  props: {
    todo: {
      type: Object,
      required: true,
    },
    index: Number,
  },
  filters: {
    upperCase(value) {
      return value.toUpperCase();
    },
  },
};
</script>

<style scoped>
  li {
    border: 1px solid #ccc;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: .5rem 2rem;
    margin-bottom: 1rem;
  }

  input {
    margin-right: 1rem;
  }

  .button-remove {
    background-color: #fff;
    border: none;
    font-size: 1.5rem;
  }

  .done {
    text-decoration: line-through;
  }
</style>
