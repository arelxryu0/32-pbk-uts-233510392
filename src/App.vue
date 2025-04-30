<template>
  <div class="container">
    <h1>Daftar Kegiatan</h1>

    <form @submit.prevent="addActivity">
      <input
        v-model="newActivity"
        type="text"
        placeholder="Masukkan kegiatan baru"
      />
      <button type="submit">Tambah</button>
    </form>

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
])

const newActivity = ref('')

const addActivity = () => {
  const trimmed = newActivity.value.trim()
  if (trimmed) {
    activities.value.push(trimmed)
    newActivity.value = ''
  }
}
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
form {
  margin-bottom: 1rem;
}
input {
  padding: 0.5rem;
  font-size: 1rem;
  width: 70%;
  margin-right: 0.5rem;
}
button {
  padding: 0.5rem 1rem;
  font-size: 1rem;
  cursor: pointer;
}
li {
  margin-bottom: 0.5rem;
}
</style>
