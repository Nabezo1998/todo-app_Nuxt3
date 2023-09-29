<template>
  <div>
    <h1>Todo</h1>
    <input type="hidden" v-model="todoInput.id"/>
    <input v-model="todoInput.name"/>
    <button @click="todoInput.id ? execUpdate() : addTask()">{{ buttonText }}</button>
    <div class='todo-list' v-for="task in taskNameList" :key="task.id">
      {{ task.name }}
      <button @click="completeTask(task.name)">完了</button>
      <button @click="fillInput(task)">更新</button>
    </div>
  </div>
</template>

<script setup lang="ts">
interface Item {
  id: number;
  name: string;
}
interface Input {
  id: number | null;
  name: string;
}
const todoInput = ref<Input>({
  id: null,
  name: '',
});
const buttonText = computed(() => {
  return todoInput.value.id ? '更新' : '追加';
});

const taskNameList = ref<Item[]>([
  {
    id: 1,
    name: "HTML",
  },
  {
    id: 2,
    name: "CSS",
  },
  {
    id: 3,
    name: "JavaScirpt",
  },
  {
    id: 4,
    name: "Vue",
  },
]);

const addTask = () => {
  if (todoInput.value.name === "") {
    return;
  }
  const newTask: Item = {
    id: taskNameList.value.length + 1,
    name: todoInput.value.name,
  };
  taskNameList.value.push(newTask);
  clearInput();
};
const completeTask = (completedTask: string) => {
  taskNameList.value = taskNameList.value.filter((task) => {
    return task.name !== completedTask;
  });
};
const fillInput = (task: Item) => {
  todoInput.value = task;
};
const execUpdate = () => {
  if (todoInput.value.name === "") {
    return;
  }
  clearInput();
};
const clearInput = () => {
  todoInput.value = {
    id: null,
    name: '',
  };
}
</script>
<style>
.todo-list {
  margin-top: 50px;
  display: flex;
  gap: 10px;
}
button {
  width: 50px;
}
</style>
