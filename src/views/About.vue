<template>
  <div class="about">
    <h1>This is an about page</h1>
    <p>{{ msg }}</p>
    <p>{{ msg2 }}</p>
    <p>{{ msg3 }}</p>
    <p>{{ add }}</p>
    <p>{{ double }}</p>
    <button @click="changeData">change</button>
    <son :add="add" @accecpet="accecpet" />
    <p>{{ accMsg }}</p>
  </div>
</template>
<script>
import {
  computed,
  provide,
  reactive,
  ref,
  toRefs,
  watch,
} from "@vue/composition-api";
import Son from "../components/son.vue";
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
  components: {
    Son,
  },
  setup() {
    const state = reactive({
      msg2: "你是一个坏蛋",
      msgSon: "provide,reject方法传值",
      double: computed(() => {
        return state.msg2 + state.msg2;
      }),
    });
    // return state;
    const msg3 = ref("加油！！");
    const accMsg = ref("传值前！！");
    // 方法
    const changeData = () => {
      console.log("METHODS");
      state.msg2 = "你是一个大坏蛋";
      msg3.value = "雅玛多"; // 显式修改
    };
    const accecpet = (value) => {
      accMsg.value = value;
    };
    // computed
    const add = computed(() => {
      return state.msg2 + msg3.value;
    });
    // watch
    watch(
      () => state.msg2,
      (newValue, oldeValue) => {
        console.log(newValue, oldeValue);
      }
    );
    // 传值
    provide("msg", state.msgSon);
    return {
      msg3,
      ...toRefs(state),
      changeData,
      accecpet,
      add,
      accMsg,
    };
  },
};
</script>
