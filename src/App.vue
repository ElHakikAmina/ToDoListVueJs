<template>
 <div class="wrapper">
  <h1> Lise to do</h1>
  <div>
    <form class="inputField" @submit.prevent="create">
      <input v-model="newTodo" autocomplete="off">
      <button>ajout</button>
    </form>
  </div>
  <ul class="todoList">
    <li v-for="item in todos" :key="item.id">
      <h3 :class="{ done : item.completed}" @click="completed(item)">{{ item.content }}</h3>
      <button @click="remove(item)">supprimer</button>
    </li>
  </ul>
  <div class="footer">
    <button @click="markAll()">selectionner tous</button>
  </div>
 </div>
</template>

<script>
import { ref } from 'vue'
export default {
  setup(){
    const todos = ref([])
    const newTodo = ref ('')
    function create (){
      todos.value.push({
        id:Date.now(),
        content:newTodo.value,
        completed:false
      })
      newTodo.value =''
      
    }
    function remove(item){
        todos.value.splice(todos.value.indexOf(item),1)
      }
    function completed(item){
      item.completed = !item.completed
    }
    function markAll()
    {
      todos.value.forEach((todo) => todo.completed = true)
    }
    return {
      todos,
      newTodo,
      create,
      remove,
      completed,
      markAll
    }
  }
}
</script>

<style>
.done{
  text-decoration:line-through;
}
</style>
