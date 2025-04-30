<template>
  <div class="container">
    <h1>Daftar Kegiatan</h1>
    <ul v-if="activities.length">
      <li v-for="(activity, index) in activities" :key="index">
        {{ activity }}
      </li>
    </ul>
    <p v-else>Tidak ada kegiatan yang tersedia.</p>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const activities = ref([
  'Belajar Vue.js',
  'Mengerjakan tugas',
  'Olahraga pagi',
  'Membaca buku'
])
</script>

<style scoped>
.container {
  max-width: 600px;
  margin: auto;
  padding: 2rem;
  font-family: sans-serif;
}
h1 {
  color: #333;
}
li {
  margin-bottom: 0.5rem;
}
</style>
