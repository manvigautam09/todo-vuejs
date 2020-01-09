<template>
  <div class="todo-array">
    <div v-for="item in todos" :key="item.id" class="todo-item">
      <div class="checked-div">
        <input type="checkbox" v-model="item.isChecked" />
      </div>
      <input
        v-if="item.editFlag"
        type="text"
        v-model="todoTask"
        @keyup.enter="onProcessEdit(item, todoTask)"
        class="todo-input-task"
      />
      <div v-else type="text" class="todo-task" @dblclick="onStartEdit(item)">
        <p v-if="!item.isChecked">{{ item.task }}</p>
        <strike v-else class="striked-text">{{ item.task }}</strike>
      </div>
      <button class="todo-del-button" @click="onDelete(item)">
        <p class="delete-text">
          <font-awesome-icon icon="times" class="icon-style" />
        </p>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "TodoArray",
  props: ["todos", "onDelete", "onStartEdit", "onEdit"],
  data() {
    return {
      todoTask: "",
      checked: ""
    };
  },
  methods: {
    onProcessEdit(item, todoTask) {
      this.onEdit(item, todoTask);
      this.todoTask = "";
    }
  }
};
</script>
<style scoped>
div.todo-array {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  max-height: 350px;
  overflow-y: scroll;
}
div.todo-item {
  background-color: white;
  display: flex;
  border-bottom: solid 1px #cccccc;
}
div.checked-div {
  width: 53px;
  border-left: solid 1px #cccccc;
  display: flex;
  justify-content: center;
  align-items: center;
}

div.round {
  position: relative;
}
strike.striked-text {
  display: block;
  margin-block-start: 1em;
  margin-block-end: 1em;
  margin-inline-start: 0px;
  margin-inline-end: 0px;
}
div.todo-task {
  width: 300px;
  height: 40px;
  font-size: 16px;
}
input.todo-input-task {
  width: 298px;
  height: 40px;
  font-size: 14px;
  border-top: none;
  border-bottom: none;
  border-width: 1px;
  border-right-color: #cccccc;
}
button.todo-del-button {
  height: 43px;
  width: 80px;
  border-left: none;
  border-top: none;
  border-bottom: none;
  border-color: #cccccc;
}
p.delete-text {
  opacity: 0;
  cursor: pointer;
  color: #e8d4d5;
  margin: 0px;
  font-size: 20px;
}
p.delete-text:hover {
  opacity: 1;
  cursor: pointer;
}
</style>
