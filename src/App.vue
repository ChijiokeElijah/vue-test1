<template>
  <div class="title">TODOS</div>

  <ul>
    <Todo
      v-for="(todo, i) in todos"
      :key="i"
      :todo="todo"
      @delete-todo="deleteTodo($event)"
      @toggle-todo="todo.isCompleted = !todo.isCompleted"
      @update-todo="todo.name = $event"
    />
  </ul>

  <div class="input-container">
    <input type="text" v-model="todo" />

    <button class="add-btn" @click="addTodo" :disabled="!todo">Add Todo</button>
  </div>
</template>

<script>
import Todo from "./components/Todo";

export default {
  name: "App",
  components: { Todo },
  data() {
    return {
      todo: "",
      todos: [
        {
          id: 1,
          name: "Buy Bread",
          isCompleted: false,
        },
      ],
    };
  },
  watch: {
    todos: {
      handler() {
        this.setTodos(this.todos);
      },
      deep: true,
    },
  },
  methods: {
    setTodos(todos) {
      localStorage.setItem("todos", JSON.stringify(todos));
    },
    getTodos() {
      const storedTodos = localStorage.getItem("todos");

      if (storedTodos) {
        return JSON.parse(storedTodos);
      }

      return [];
    },
    addTodo() {
      this.todos.push({
        id: this.todos.length + 1,
        name: this.todo,
        isCompleted: false,
      });
      // add it to localstorage here
      // this.setTodos(this.todos);
      this.todo = "";
    },
    updateTodo() {},
    deleteTodo(id) {
      this.todos = this.todos.filter((todo) => todo.id !== id);
      // add it to localstorage here
      // this.setTodos(this.todos);
    },
  },
  beforeCreate() {
    console.log("parent, beforeCreate");
  },
  created() {
    console.log("parent, created");
  },
  beforeMount() {
    console.log("parent, beforeMount");
  },
  mounted() {
    console.log("parent, Mounted");
    this.todos = this.getTodos();
  },
  updated() {},
  beforeUpdate() {},
  beforeUnmount() {},
  unmounted() {},
};
</script>

<style>
.title {
  margin-bottom: 15px;
  font-size: 18px;
  font-weight: 600;
}

.add-btn {
  margin-left: 5px;
}

.delete-btn {
  margin-right: 5px;
  margin-left: 20px;
}

.input-container {
  margin-top: 20px;
}

.todo-item {
  margin-bottom: 10px;
}

.has-line-through {
  text-decoration: line-through;
}
</style>
