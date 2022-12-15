<template>
  <li class="todo-item">
    <span :class="[todo.isCompleted ? 'has-line-through' : '']">
      👉
      <input type="text" @input="handleChange" :value="todo.name" />
    </span>

    <button class="delete-btn" @click="$emit('delete-todo', todo.id)">
      Delete
    </button>

    <button @click="$emit('toggle-todo')">
      {{ todo.isCompleted ? "Undo" : "Complete" }}
    </button>
  </li>
</template>

<script>
export default {
  props: ["todo"],
  data() {
    return {};
  },
  methods: {
    handleChange(event) {
      this.$emit("update-todo", event.target.value);
    },
  },
  beforeCreate() {
    console.log("child, beforeCreate");
  },
  created() {
    console.log("child, create");
  },
  beforeMount() {
    console.log("child, beforeMount");
  },
  mounted() {
    console.log("child, Mounted");
  },
  updated() {},
  beforeUpdate() {},
  beforeUnmount() {},
  unmounted() {},
};
</script>

<style>
</style>