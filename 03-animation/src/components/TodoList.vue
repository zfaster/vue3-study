<template>
  <div>
    <input type="text" v-model="title" @keydown.enter="addTodo" />
    <button v-if="active<all" @click="clear">清理</button>
    <ul v-if="todos.length">
      <transition-group name="flip-list" tag="ul">
      <li v-for="todo in todos" >

        <input type="checkbox" v-model="todo.done" />
        <span :class="{done: todo.done}">{{todo.title}}</span>
      </li>
      </transition-group>
    </ul>
    <div v-else>暂无数据</div>
    <div>
      全选 <input type="checkbox" v-model="allDone" />
      <span>{{active}}/{{all}}</span>
    </div>
    <transition name="modal">
    <div class="info-wrapper" v-if="showModal">
      <div class="info">
        哥，你啥也没输入！
      </div>
    </div>
    </transition>
  </div>
</template>
<script setup>

import {computed, ref} from "vue";

let title = ref("");
let showModal = ref(false)
let todos = ref([
  {id: 1, title: "吃饭", done: false},
  {id: 2, title: "睡觉", done: false},
  {id: 3, title: "打豆豆", done: true},
]);
function addTodo() {
  if(!title.value){
    showModal.value = true
    setTimeout(()=>{
      showModal.value = false
    },1500)
    return
  }
  todos.value.push({
    id: todos.value.length + 1,
    title: title.value,
    done: false
  });
  title.value = "";
}
function clear() {
  todos.value = todos.value.filter(todo => !todo.done);
}
let  active = computed(() => todos.value.filter(todo => !todo.done).length);

let all = computed(() => todos.value.length);
let allDone = computed({
  get: () => active.value === 0,
  set: (value) => {
    todos.value.forEach(todo => todo.done = value);
  }
});
</script>

<style>
h1 {
  color: red
}
.info-wrapper {
  position: fixed;
  top: 20px;
  width:200px;
}
.info {
  padding: 20px;
  color: white;
  background: #d88986;
}
.modal-enter-from {
  opacity: 0;
  transform: translateY(-60px);
}
.modal-enter-active {
  transition: all 0.3s ease;
}
.modal-leave-to {
  opacity: 0;
  transform: translateY(-60px);
}
.modal-leave-active {
  transition: all 0.3s ease;
}
.flip-list-move {
  transition: transform 0.8s ease;
}
.flip-list-enter-active,
.flip-list-leave-active {
  transition: all 1s ease;
}
.flip-list-enter-from,
.flip-list-leave-to {
  opacity: 0;
  transform: translateX(30px);
}
</style>
