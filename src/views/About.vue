<template>
  <div class="about">
    <h1>This is an about page</h1>
    <p>{{ msg }}</p>
    <p>{{ msg2 }}</p>
    <p>{{ msg3 }}</p>
    <p>{{ add }}</p>
    <p>{{ double }}</p>
    <button @click="changeData">change</button>
  </div>
</template>
<script>
import { computed, reactive, ref, toRefs } from "@vue/composition-api";
export default {
  /**
   * vue2.x
   */
  data() {
    return {
      msg: "对不起，我是一个警察",
    };
  },
  /**
   * vue3.0
   */
  setup() {
    const state = reactive({
      msg2: "你是一个坏蛋",
      double: computed(() => {
        return state.msg2 + state.msg2;
      }),
    });
    // return state;
    const msg3 = ref("加油！！");
    // 方法
    const changeData = () => {
      console.log("METHODS");
      state.msg2 = "你是一个大坏蛋";
      msg3.value = "雅玛多"; // 显式修改
    };
    // computed
    const add = computed(() => {
      return state.msg2 + msg3.value;
    });
    return {
      msg3,
      ...toRefs(state),
      changeData,
      add,
    };
  },
};
</script>
