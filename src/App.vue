<template>
  <div id="root">
    <div class="todo-container">
      <div class="todo-wrap">
        <MyHeader :addTodo="addTodo"></MyHeader>
        <MyList :todos="todos" :checkTodo="checkTodo" :deleteTodo="deleteTodo"></MyList>
        <MyFooter :todos="todos"></MyFooter>
      </div>
    </div>
  </div>
</template>

<script>
import MyHeader from "./components/MyHeader.vue";
import MyList from "./components/MyList.vue";
import ListItem from "./components/ListItem.vue";
import MyFooter from "./components/MyFooter.vue";
export default {
  data() {
    return {
      todos: [
        { id: "001", title: "吃饭", done: true },
        { id: "002", title: "睡觉", done: false },
        { id: "003", title: "写代码", done: true },
        { id: "004", title: "看电视", done: false },
      ],
    };
  },
  components: { MyHeader, MyList, ListItem, MyFooter },
  methods: {
    addTodo(todoObj) {
      this.todos.unshift(todoObj);
    },
    checkTodo(id) {
      this.todos.forEach((todo) => {
        // console.log(todo);   //遍历的每一项todo
        if (todo.id === id) {
          // 遍历的某一项的id = 点击的id 那么就取反
          return (todo.done = !todo.done);
        }
      });
    },
    deleteTodo(id) {
      // 由于filter不改变data中的原数组，需要把过滤出来的新数组 = 赋值给原数组 
      this.todos = this.todos.filter((todo)=>{
        // 过滤出来的数组的条件
        return todo.id !== id // 不是我删除的的那个id被过滤下来
      }
      )
    },
  },
};
</script>

<style scoped>
/*base*/
body {
  background: #fff;
}

.btn {
  display: inline-block;
  padding: 4px 12px;
  margin-bottom: 0;
  font-size: 14px;
  line-height: 20px;
  text-align: center;
  vertical-align: middle;
  cursor: pointer;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2),
    0 1px 2px rgba(0, 0, 0, 0.05);
  border-radius: 4px;
}

.btn-danger {
  color: #fff;
  background-color: #da4f49;
  border: 1px solid #bd362f;
}

.btn-danger:hover {
  color: #fff;
  background-color: #bd362f;
}

.btn:focus {
  outline: none;
}

.todo-container {
  width: 600px;
  margin: 0 auto;
}
.todo-container .todo-wrap {
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
}
</style>
