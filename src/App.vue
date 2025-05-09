<template>
  <div class="app-container">
    <h1 class="title">🌊🦈 Kegiatan Anak Pulau</h1>

    <div class="form-container">
      <input
        v-model="newTask"
        @keyup.enter="addTask"
        type="text"
        placeholder="Tambahkan kegiatan baru..."
        class="input-task"
      />
      <button @click="addTask" class="btn-add">Tambah</button>
    </div>

    <div class="filter-container">
      <label>
        <input type="checkbox" v-model="showOnlyIncomplete" />
        Tampilkan hanya yang belum selesai
      </label>
    </div>

    <ul class="task-list">
      <li
        v-for="(task, index) in filteredTasks"
        :key="index"
        :class="['task-item', { done: task.done }]">
        <input type="checkbox" v-model="task.done" />
        <span class="task-text">{{ task.text }}</span>
        <button class="btn-delete" @click="removeTask(index)">❌</button>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';

const newTask = ref('');
const showOnlyIncomplete = ref(false);
const tasks = ref([
  { text: 'Beribadah', done: false },
  { text: 'Belajar', done: false },
  { text: 'Berpetualang', done: true },
  { text: 'Berburu', done: true }, 
  { text: 'Melestarikan Budaya Lokal', done: true }
]);

const filteredTasks = computed(() => {
  return showOnlyIncomplete.value
    ? tasks.value.filter((task) => !task.done)
    : tasks.value;
});

function addTask() {
  if (newTask.value.trim() === '') return;
  tasks.value.push({ text: newTask.value, done: false });
  newTask.value = '';
}

function removeTask(index) {
  tasks.value.splice(index, 1);
}
</script>