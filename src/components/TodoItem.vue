<template>
  <li>
    <label>
      <input
        type="checkbox"
        :checked="todo.done"
        @change="handleCheck(todo.id)"
      />
      <span v-show="!todo.isEdit">{{ todo.title }}</span>
      <input
        type="text"
        v-show="todo.isEdit"
        :value="todo.title"
        @blur="handleBlur(todo, $event)"
        ref="inputTitle"
      />
    </label>
    <button class="btn btn-danger" @click="handleDelete(todo.id)">
      刪除
    </button>
    <button
      class="btn btn-edit"
      v-show="!todo.isEdit"
      @click="handleEdit(todo)"
    >
      編輯
    </button>
  </li>
</template>

<script>
export default {
  name: "Item",
  // 接收todo
  props: ["todo"],
  methods: {
    //勾選
    handleCheck(id) {
      // 通知App組件將對應todo的done值取反
      this.$bus.$emit("checkTodo", id);
    },
    //刪除
    handleDelete(id) {
      if (confirm("確定要刪除嗎?")) {
        this.$bus.$emit("deleteTodo", id);
      }
    },
    //編輯
    handleEdit(todo) {
      if (Object.prototype.hasOwnProperty.call(todo, "isEdit")) {
        todo.isEdit = true;
      } else {
        //todo身上沒有isEdit
        this.$set(todo, "isEdit", true);
      }
      this.$nextTick(function() {
        this.$refs.inputTitle.focus();
      });
    },
    // 失焦後回調 (真正執行修改邏輯)
    handleBlur(todo, e) {
      todo.isEdit = false;
      if (!e.target.value.trim()) return alert("你啥都沒寫呢!");
      this.$bus.$emit("updateTodo", todo.id, e.target.value);
    },
  },
};
</script>

<style scoped>
/*item*/
li {
  list-style: none;
  height: 36px;
  line-height: 36px;
  padding: 0 5px;
  border-bottom: 1px solid #ddd;
}
li label {
  float: left;
  cursor: pointer;
}
li label li input {
  vertical-align: middle;
  margin-right: 6px;
  position: relative;
  top: -1px;
}
li button {
  float: right;
  display: none;
  margin-top: 3px;
}
li:before {
  content: initial;
}
li:last-child {
  border-bottom: none;
}
li:hover {
  background-color: #ddd;
}
li:hover button {
  display: block;
}
</style>
