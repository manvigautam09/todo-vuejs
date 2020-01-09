<template>
  <div class="outer-div">
    <div class="todo-section">
      <h1 class="heading">{{ title }}</h1>
      <div class="add-todo-div">
        <input
          v-model.trim="newTodo"
          type="text"
          class="todo-input"
          placeholder="What needs to be done?"
          @keyup.enter="submitTodo()"
        />
        <button
          class="todo-submit-button"
          @click="submitTodo()"
          :disabled="findDisabled()"
        >
          {{ btnText }}
        </button>
      </div>
      <TodoArray
        :todos="todos"
        :onDelete="onDelete"
        :onStartEdit="onStartEdit"
        :onEdit="onEdit"
      />
      <div class="todo-details">
        <h4>Total: {{ todos.length }}</h4>
        <h4>Completed: {{ computeIsCompleted() }}</h4>
        <h4>Remaining: {{ todos.length - computeIsCompleted() }}</h4>
      </div>
    </div>
  </div>
</template>
<script>
import TodoArray from "./TodoArray";

export default {
  name: "Todo",
  components: { TodoArray },

  data() {
    return {
      newTodo: "",
      todos: [],
      btnText: "Add",
      title: "ToDoS"
    };
  },
  methods: {
    submitTodo() {
      let regX = /^\s*$/;
      if (!this.newTodo || regX.test(this.newTodo)) {
        return;
      }
      let todo = {};
      todo.task = this.newTodo;
      todo.isChecked = false;
      todo.editFlag = false;
      todo.id = Date.now();
      this.todos.push(todo);
      this.newTodo = "";
    },
    findDisabled() {
      let regX = /^\s*$/;
      if (!this.newTodo || regX.test(this.newTodo)) return true;
      return false;
    },
    onDelete(item) {
      let newTodos = this.todos;
      newTodos = newTodos.filter(todo => {
        return todo.id !== item.id;
      });
      this.todos = newTodos;
    },
    onStartEdit(item) {
      const newTodos = this.todos;
      newTodos.forEach(todo => {
        if (todo.id === item.id) {
          todo.editFlag = true;
        }
      });
    },
    onEdit(item, newTask) {
      const newTodos = this.todos;
      newTodos.forEach(todo => {
        if (todo.id === item.id) {
          todo.task = newTask;
          todo.editFlag = false;
        }
      });
      newTask = "";
    },
    computeIsCompleted() {
      const newTodos = this.todos;
      let count = 0;
      newTodos.forEach(todo => {
        if (todo.isChecked) {
          count += 1;
        }
      });
      return count;
    }
  }
};
</script>
<style scoped>
div.outer-div {
  justify-content: center;
  align-items: center;
  display: flex;
  flex-direction: column;
  padding-top: 50px;
}
div.todo-section {
  display: flex;
  flex-direction: column;
  background-color: #e8d4d5;
  width: 470px;
}
h1.heading {
  align-self: center;
}
div.add-todo-div {
  display: flex;
  justify-content: center;
  align-items: center;
}
input.todo-input {
  width: 350px;
  height: 40px;
  font-size: 20px;
}
button.todo-submit-button {
  height: 45px;
  width: 80px;
  border-radius: 5px;
  background-color: #f2eded;
}
div.todo-details {
  display: flex;
  align-items: center;
  justify-content: space-around;
}
</style>
