<template>
  <header class="header">
    <h1>todos</h1>
    <input id="toggle-all" class="toggle-all" type="checkbox" v-model="isAll" />
    <label for="toggle-all"></label>
    <!-- 3.0 键盘事件-回车按键
         3.1 输入框 - v-model获取值
     -->
    <input
      class="new-todo"
      placeholder="输入任务名称-回车确认"
      autofocus
      @keyup.enter="addBtn"
      v-model="task"
    />
  </header>
</template>

<script>
export default {
  data() {
    return {
      task: "", //用于接收任务表单的值
    };
  },
  methods: {
    addBtn() {
      //3.2 当前任务的名字要加入到list数组中
      //子传父技术
      this.$emit("create", this.task);
      this.task = "";
    },
  },
  computed: {
    isAll: {
      // 全选框改变小复选框
      set(checked) {
        return this.arr.forEach((obj) => (obj.isDone = checked));
      },
      // 小复选框影响全选框
      //! 如果数组为空，every会直接返回true
      get() {
        return (
          this.arr.length !== 0 && this.arr.every((obj) => obj.isDone === true)
        );
      },
    },
  },
  props: ["arr"],
};
</script>