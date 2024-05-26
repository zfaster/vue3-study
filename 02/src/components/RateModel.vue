<script setup>
import {defineProps, computed, ref} from 'vue';
let props = defineProps({
  modelValue: Number,
  theme: {type:String,default:'red'}
})
const fontstyle = computed(() => {
  return {
    color: props.theme,
    fontSize: '20px'
  }
})
// 评分宽度
let width = ref(props.modelValue)
function mouseOver(i){
  width.value = i
}
function mouseOut(){
  width.value = props.modelValue
}
const fontwidth = computed(()=>`width:${width.value}em;`)
let emits = defineEmits(['update:modelValue'])
function onRate(i){
  emits('update:modelValue', i)
}
</script>

<template>
  <div :style="fontstyle">
    <slot></slot>
    <div class='rate' @mouseout="mouseOut">
      <span @mouseover="mouseOver(num)"  v-for='num in 5' :key="num">☆</span>
      <span class='hollow' :style="fontwidth">
        <span @click="onRate(num)" @mouseover="mouseOver(num)" v-for='num in 5' :key="num">★</span>
      </span>
    </div>
  </div>
</template>


<style scoped>
.rate{
  position:relative;
  display: inline-block;
}
.rate > span.hollow {
  position:absolute;
  display: inline-block;
  top:0;
  left:0;
  width:0;
  overflow:hidden;
}
</style>
