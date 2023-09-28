<template>
  <div>
    <h1>Todo App</h1>
    <input v-model="taskName">
    <button @click="taskName ? execUpdate(): addTask()">{{ buttonText }}</button>
    <div
      v-for="task in taskNameList"
      :key="task"
    >
      {{ task }}
      <button @click="completeTask(task)">削除</button>
      <button @click="changeTask(task)">更新</button>
    </div>
  </div>
</template>

<script setup lang="ts">
  const taskName = ref<string>('');
  const buttonText = computed(() => {
    return 
  })
  const taskNameList =ref<string[]>(['html', 'css', 'Java Script']);
  const addTask = () => {
    if (taskName.value === '') {
      return;
    }
    taskNameList.value.push(taskName.value);
    taskName.value = '';
  }
  const completeTask = (completedTask:string) => {
    taskNameList.value = taskNameList.value.filter((taskName:string) => {
      return taskName !== completedTask;
    })
  }
const changeTask = (task:string) => {
  taskName.value = task;
}
const execUpdate = () => {
  console.log('更新するよ');
  
  if (taskName.value === '') {
      return;
  }
}


</script>