<template>
  <div>
    <h1 @click="add">{{count}}</h1>
  </div>
  坐标
  <div>x:{{x}},y:{{y}}</div>

</template>

<script setup>
import { ref } from "vue";
import {useMouse} from "@/utils/mouse.js";
let count = ref(0);
let color = ref("red");
let {x,y} =useMouse()
function add() {
  count.value++;
  color.value = count.value % 2 === 0 ? "red" : "blue";
}
</script>
<style scoped>
h1 {
  color: v-bind(color)
}
</style>
