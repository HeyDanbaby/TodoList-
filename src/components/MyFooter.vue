<template>
  <!-- 整个footer在没有todo项的时候不显示  -->
  <!-- 
    v-show=true 显示 / false 不显示
    total>0 >0的数字转为布尔值为true 显示
    total=0 0转为布尔值为false 不显示
  -->
  <div v-show="total" class="todo-footer">
    <label>
      <!-- <input type="checkbox" :checked="isAll" @click="checkAll"/> -->
      <input type="checkbox" v-model="isAll" />
    </label>
    <span>
      <span>已完成{{ doneTotal }}</span> / 全部{{ total }}
    </span>
    <button class="btn btn-danger" @click="clearAll">清除已完成任务</button>
  </div>
</template>

<script>
export default {
  props: ["todos", "checkAllTodo", 'clearAllTodo'],
  computed: {
    total() {
      return this.todos.length;
    },
    doneTotal() {
      // 简写：
      return this.todos.reduce((pre, todo) => {
        return pre + (todo.done ? 1 : 0);
      }, 0);

      // 方法1：forEach()
      // let i = 0;
      // this.todos.forEach((todo) => {
      //   if (todo.done) {
      //     return i++;
      //   }
      // });
      // return i;
      // 方法2：reduce()解析
      // const x = this.todos.reduce((pre, current) => {
      //   // 函数体被执行todos.length=4次
      //   console.log(pre, current);  // 0, id: "001" => return 0+1=1
      //   // console.log(pre,current) // 1, id: "002" => return 1+1=2
      //   // console.log(pre,current) // 2, id: '003' => return 2+1=3
      //   // console.log(pre,current) // 3, id: '004' => return 3+1=4 作为最终的函数返回值
      //   return pre + 1;
      // }, 0);
      // console.log(x)  // 4
      // 以上分析：pre就是上一次返回的值，current就是当前每一个todo对象
      // const x = this.todos.reduce((pre, todo) => {
      //   return pre + (todo.done ? 1 : 0);
      // }, 0);
      // console.log(x)

      // 复习reduce()方法
      // let arr = [1, 2, 3, 4];
      // let initValue = 0;
      // const a = arr.reduce((preValue, currentValue) => {
      //   return preValue + currentValue;
      // }, initValue);
      // console.log(a);
    },
    isAll: {
      // 1、函数式写法：return this.doneTotal === this.total && this.total > 0;
      // 2、完整写法 set、get
      // checkbox勾选框被读取了调用getter
      get() {
        return this.doneTotal === this.total && this.total > 0;
      },
      // checkbox勾选框被修改了调用setter
      set(value) {
        // console.log(value);  // true/false
        // 通知父组件全选or全不选
        this.checkAllTodo(value);
      },
    },
   
  },
  methods: {
    // checkAll(e) {
    //   // 判断checkbox勾选框是否勾选 勾选true 未勾选false
    //   // 勾选框：e.target.checked
    //   // 输入框：e.target.value
    //   // console.log(e.target.checked)
    //   this.checkAllTodo(e.target.checked);
    // },

    clearAll(){
      this.clearAllTodo()
    }
  },
};
</script>

<style scoped>
/*footer*/
.todo-footer {
  height: 40px;
  line-height: 40px;
  padding-left: 6px;
  margin-top: 5px;
}

.todo-footer label {
  display: inline-block;
  margin-right: 20px;
  cursor: pointer;
}

.todo-footer label input {
  position: relative;
  top: -1px;
  vertical-align: middle;
  margin-right: 5px;
}

.todo-footer button {
  float: right;
  margin-top: 5px;
}
</style>
