<template>
  <div class="todo-header">
    <input
      type="text"
      placeholder="请输入你的任务名称，按回车键确认"
      v-model="title"
      @keyup.enter="add"
    />
  </div>
</template>

<script>
import { nanoid } from "nanoid";

export default {
  data() {
    return {
      title: "",
    };
  },
  props: ["addTodo"],
  methods: {
    // add(e) {
    //   const todoObj = { id: nanoid(), title: e.target.value, done: false };
    //   console.log(todoObj); // 添加的对象
    //   this.addTodo(todoObj)  // 调用父传过来的方法 ，并且把父需要的数据作为参数传过去
    //   e.target.value = ''
    // },
    add() {
      if (!this.title.trim()) {
        return alert("输入不能为空");
      }
      const todoObj = { id: nanoid(), title: this.title, done: false };
      this.addTodo(todoObj);
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
