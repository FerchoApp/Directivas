<script setup>
import { ref } from 'vue';

let newTask = ref('')
let taskList = ref([
{
  name: 'Estudiar',
  done: false
},

{
  name: 'Comer',
  done: false
},

{
  name: 'Dormir',
  done: false
}])

function addTask(){
  if(newTask.value.trim() == ''){
    return
  }
  taskList.value.push({
    name: newTask.value,
    done: false
  })
  newTask.value=''
}

function setDone(index){
  taskList.value[index].done = true
}

</script>

<template>
<div class="container">

  <h1>Lista de tareas</h1>
  <p class="subtitule">{{ newTask }}</p>

    <div>
      <div class="task" :class="{done: task.done}" v-for="(task, index) in taskList" :key="index"> {{ task.name }} <span @click="setDone(index)" class="button">❌</span></div>
    </div>

  <input v-model="newTask" @keypress.enter="addTask" type="text" placeholder="Escriba su tarea">
  <p v-show="newTask != ''" class="help">presiona enter para agregar la tarea</p>

</div>
</template>

<style scoped>
.done{
  text-decoration: line-through;
}

.container {
  padding: 6px 12px;
  font-family: 'Noto Sans KR', sans-serif;
  color: #F2F2F2;
  background-color: #044040;
  border-radius: 15px;
  max-width: 420px;
  margin: 0 auto;
}

h1 {
  text-transform: uppercase;
  font-size: 25px;
  text-align: center;
  margin-bottom: 0;
}

.subtitule {
  margin: 0;
  margin-bottom: 16px;
  text-align: center;
  opacity: 0.5;
  font-size: 15px;
}

.task {
  display: flex;
  justify-content: space-between;
  background-color:#591C21;
  border-radius: 10px;
  margin-bottom: 2px;
  padding: 2px 2px 1px 2px;
}

.task:hover{
  background-color:#D92525;
}

.button{
  background-color:#8C1F28;
  display: inline-block;
  padding: 0 6px;
  border-radius: 10px;
}

.button:hover{
  cursor: pointer;
}

input{
  border: none;
  border-radius: 3px;
  padding: 2px 6px;
  outline: none;
  /* width: calc(100% - 12px);*/
  box-sizing: border-box;
  width: 100%;
}

input::placeholder{
  opacity: 0.5;
}

.help{
  font-size: 10px;
  opacity: 0.6;
  margin: 0;
}

</style>
