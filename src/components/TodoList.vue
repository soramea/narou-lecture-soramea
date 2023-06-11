<script setup lang="ts">
import { ref } from 'vue'

interface Tasks {
  name: string
  done: boolean
}

const tasks = ref<Tasks[]>([])
const newTaskName = ref('')

const addTask = () => {
  if (newTaskName.value != '') {
    tasks.value.push({ name: newTaskName.value, done: false })
  }
  newTaskName.value = ''
}
</script>

<template>
  <div>
    <div>TaskList</div>
    <ul>
      <li v-for="task in tasks" :key="task.name" :class="{ finished: task.done == true }">
        <div>{{ task.name }}</div>
        <div v-if="task.done == false">
          <button @click="task.done = true">完了！</button>
        </div>
      </li>
    </ul>
    <div>
      <label>
        タスク名
        <input v-model="newTaskName" type="text" />
      </label>
      <button @click="addTask">add</button>
    </div>
  </div>
</template>

<style>
.finished {
  color: lightgray;
}
</style>
