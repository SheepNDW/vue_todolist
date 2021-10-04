<template>
  <div class="todo-header">
    <input
      type="text"
      placeholder="輸入你的待辦事項, 按Enter確認"
      v-model="title"
      @keyup.enter="add"
    />
  </div>
</template>

<script>
import { nanoid } from "nanoid";
export default {
  name: "TodoHeader",
  data() {
    return {
      title: "",
    };
  },
  methods: {
    add() {
      // 防呆
      if (!this.title.trim()) return alert("你還沒輸入東西呀!");
      // 把輸入值包裝成todo對象
      const todoObj = { id: nanoid(), title: this.title, done: false };
      this.$emit("addTodo", todoObj);
      this.title = "";
    },
  },
};
</script>

<style scoped>
/*header*/
.todo-header input {
  width: 560px;
  height: 28px;
  font-size: 14px;
  border: 1px solid #ccc;
  border-radius: 4px;
  padding: 4px 7px;
}
.todo-header input:focus {
  outline: none;
  border-color: rgba(82, 168, 236, 0.8);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075),
    0 0 8px rgba(82, 168, 236, 0.6);
}
</style>
