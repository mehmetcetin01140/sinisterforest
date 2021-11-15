<template>
  <div id="app">
    <comp-one></comp-one>
    <comp-two></comp-two>
  </div>
</template>

<script>
import CompOne from "./CompOne.vue";
import CompTwo from "./CompTwo.vue";
import { eventBus } from "./main";
export default {
  name: "app",
  components: {
    CompOne,
    CompTwo
  }
};
</script>

<style></style>
