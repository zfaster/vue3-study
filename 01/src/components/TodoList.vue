<template>
  <div>
    <input type="text" v-model="title" @keydown.enter="addTodo" />
    <button v-if="active<all" @click="clear">清理</button>
    <ul v-if="todos.length">
      <li v-for="todo in todos" >

        <input type="checkbox" v-model="todo.done" />
        <span :class="{done: todo.done}">{{todo.title}}</span>
        <button @click="remove(todo)">删除</button>
      </li>
    </ul>
    <div v-else>暂无数据</div>
    <div>
      全选 <input type="checkbox" v-model="allDone" />
      <span>{{active}}/{{all}}</span>
    </div>
  </div>
</template>
<script setup>

import {computed, ref} from "vue";

let title = ref("");
let todos = ref([
  {id: 1, title: "吃饭", done: false},
  {id: 2, title: "睡觉", done: false},
  {id: 3, title: "打豆豆", done: true},
]);
function addTodo() {
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
</style>
