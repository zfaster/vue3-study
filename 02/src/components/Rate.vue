<script setup>
import { defineProps,computed } from 'vue';
let props = defineProps({
  value: Number,
  theme: {type:String,default:'red'}
})
let rate = computed(()=>"★★★★★☆☆☆☆☆".slice(5 - props.value, 10 - props.value))
const fontstyle = computed(() => {
  return {
    color: props.theme,
    fontSize: '20px'
  }
})
</script>

<template>
  <div :style="fontstyle">
    {{rate}}
  </div>
</template>


<style scoped>

</style>
