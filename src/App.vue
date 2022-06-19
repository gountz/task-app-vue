<script setup>
  import { ref } from 'vue';
  import Input from './components/Input.vue';
  import Todos from './components/Todos.vue';
  import './assets/styles/app.css'

  const todos = ref([]);
  const name = ref('');
  const add = ($event) => {
    if(!todos.value.some(vl => vl.title === $event)){
      const task = { title: $event, done: false, edit: false, createdAt: Date.now()};
      todos.value.push(task);
    }
  }
  const onDeleteTask = ($event) => {
    todos.value = todos.value.filter(vl => vl.title !== $event.title)
  }
  const changeStatus = ($event) => {
    todos.value = todos.value.map(vl => {vl.done = vl.title === $event.title ? $event.done : vl.done; return vl})
  }
  const editTitle = ($event) => {
    if($event.title !== ''){
      todos.value = todos.value.map(vl => {
        vl.title = vl.title === $event.original ? $event.title : vl.title;
        vl.edit = vl.title === $event.original ? false : vl.edit;
        return vl;
      })
    }
  }
</script>

<template>
  <main class="app">
    <section class="section-page">
      <article class="article-input">
        <Input :name="name" @catchTask="add" />
      </article>
      <Todos :todos="todos" @deleteTask="onDeleteTask" @newStatus="changeStatus" @editTle="editTitle"/>
    </section>
  </main>
</template>