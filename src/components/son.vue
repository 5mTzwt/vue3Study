<template>
  <div>
    <h2>我是子组件</h2>
    <p>{{ add }}</p>
    <p>{{ msg }}</p>
    <button @click="toFather">给父组件传值</button>
  </div>
</template>

<script>
import { inject, reactive, toRefs, emit } from "@vue/composition-api";
export default {
  props: ["add"], // 这个必须有
  setup(props, context) {
    const state = reactive({
      featherMsg: "传值后！！！",
      myAdd: props.add,
      msg: inject("msg"),
    });
    const toFather = () => {
      context.emit("accecpet", state.featherMsg);
    };
    return {
      ...toRefs(state),
      toFather,
    };
  },
};
</script>

<style></style>
