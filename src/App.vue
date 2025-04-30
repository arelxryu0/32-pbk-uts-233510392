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
        <input
          type="checkbox"
          v-model="activity.done"
        />
        <span :class="{ done: activity.done }">{{ activity.name }}</span>
        <button class="delete" @click="removeActivity(index)">Batalkan</button>
      </li>
    </ul>
    <p v-else>Tidak ada kegiatan yang tersedia.</p>
  </div>
</template>

<script setup>
import { ref } from 'vue'

// Menyimpan kegiatan sebagai objek dengan properti `done`
const activities = ref([
  { name: 'Belajar Vue.js', done: false },
  { name: 'Mengerjakan tugas', done: false },
  { name: 'Olahraga pagi', done: false },
  { name: 'Membaca buku', done: false }
])

const newActivity = ref('')

const addActivity = () => {
  const trimmed = newActivity.value.trim()
  if (trimmed) {
    activities.value.push({ name: trimmed, done: false })
    newActivity.value = ''
  }
}

const removeActivity = (index) => {
  activities.value.splice(index, 1)
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
input[type="text"] {
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
.delete {
  margin-left: 1rem;
  background-color: #ff4d4d;
  color: white;
  border: none;
  border-radius: 4px;
}
li {
  margin-bottom: 0.5rem;
  display: flex;
  align-items: center;
}
li input[type="checkbox"] {
  margin-right: 0.5rem;
}
.done {
  text-decoration: line-through;
  color: #888;
}
</style>
