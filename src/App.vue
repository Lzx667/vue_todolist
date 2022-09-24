<template>
  <div class="todoapp">
    <!-- 1.3 使用组件 -->
    <!-- 3.3 定义一个自定义事件用于触发子传过来的数据 -->
    <TodoHeader @create="createFn" :arr="list"></TodoHeader>
    <TodoMain :arr="showAll" @del="deleteFn"></TodoMain>
    <TodoFooter
      :farr="showAll"
      @changeType="typeFn"
      @clear="clearFn"
    ></TodoFooter>
  </div>
</template>

<script>
// 1. 目标: 创建工程-准备相关组件文件-标签+样式 (静态)
// 1.0 引入样式
import "./styles/base.css";
import "./styles/index.css";
// 1.1 引入组件
import TodoHeader from "./components/TodoHeader.vue";
import TodoMain from "./components/TodoMain.vue";
import TodoFooter from "./components/TodoFooter.vue";
export default {
  // 1.2 注册组件
  components: {
    TodoHeader,
    TodoMain,
    TodoFooter,
  },
  data() {
    return {
      list: JSON.parse(localStorage.getItem("todoList")) || [],
      getsel: "all",
    };
  },
  methods: {
    createFn(taskName) {
      //添加任务
      const id =
        this.list.length > 0 ? this.list[this.list.length - 1].id + 1 : 100;
      this.list.push({
        id,
        name: taskName,
        isDone: false,
      });
    },
    deleteFn(theid) {
      //删除任务
      const index = this.list.findIndex((obj) => obj.id === theid);
      this.list.splice(index, 1);
    },
    typeFn(str) {
      // 定义一个全局变量用于接收
      this.getsel = str;
    },
    clearFn() {
      // 清除已完成
      this.list = this.list.filter((obj) => obj.isDone === false);
    },
  },
  computed: {
    // 6.5 定义showArr数组 - 通过list配合条件筛选而来
    showAll() {
      if (this.getsel === "yes") {
        //显示已完成
        return this.list.filter((obj) => obj.isDone === true);
      } else if (this.getsel === "no") {
        return this.list.filter((obj) => obj.isDone === false);
      } else return this.list;
    },
  },

  // 目标数据缓存
  // 开启深度缓存
  watch: {
    list: {
      deep: true,
      handler() {
        // 只要list 发生变化 --就覆盖式的保存到本地存储中
        localStorage.setItem("todoList", JSON.stringify(this.list));
      },
    },
  },
};
</script>

<style>
</style>