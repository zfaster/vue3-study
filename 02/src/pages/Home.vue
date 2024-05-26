<template>
  <h1>这是首页</h1>
  <rate :value="2"/>
  <rate :value="3" theme="blue"/>
  <rate-event :value="score" theme="blue" @update-rate="update"/>
  <rate-model v-model="score" theme="blue">哈哈</rate-model>
</template>
<script setup lang="ts">
import Rate from "@/components/Rate.vue";
import RateEvent from "@/components/RateEvent.vue";
import {ref} from "vue";
import RateModel from "@/components/RateModel.vue";

let score = ref(3.5)
function update(value:number){
  score.value = value
}
</script>
