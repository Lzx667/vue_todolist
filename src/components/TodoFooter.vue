<template>
  <footer class="footer">
    <span class="todo-count"
      >剩余<strong>{{ count }}</strong></span
    >
    <ul class="filters" @click="fn">
      <li>
        <a
          :class="{ selected: isSel === 'all' }"
          href="javascript:;"
          @click="isSel = 'all'"
          >全部</a
        >
      </li>
      <li>
        <a
          :class="{ selected: isSel === 'no' }"
          href="javascript:;"
          @click="isSel = 'no'"
          >未完成</a
        >
      </li>
      <li>
        <a
          :class="{ selected: isSel === 'yes' }"
          href="javascript:;"
          @click="isSel = 'yes'"
          >已完成</a
        >
      </li>
    </ul>
    <button class="clear-completed" @click="clearFn">清除已完成</button>
  </footer>
</template>

<script>
export default {
  props: ["farr"],
  //为了练习一下计算属性就不直接使用数组的长度了
  computed: {
    count() {
      return this.farr.length;
    },
  },
  data() {
    return {
      isSel: "all",
    };
  },
  methods: {
    fn() {
      //切换筛选条件
      //  子传父
      this.$emit("changeType", this.isSel);
    },
    clearFn() {
      //清除已完成
      //子传父
      this.$emit("clear");
    },
  },
};
</script>