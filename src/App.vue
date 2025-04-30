<template>
  <div class="page">
    <div class="container">
      <h1>📋 Daftar Kegiatan</h1>

      <form @submit.prevent="addActivity" class="input-group">
        <input
          v-model="newActivity"
          type="text"
          placeholder="➕ Tambah kegiatan baru..."
        />
        <button type="submit" title="Tambah Kegiatan">
          <span>➕</span>
        </button>
      </form>

      <div class="filter">
        <label>
          <input type="checkbox" v-model="showOnlyIncomplete" />
          Tampilkan hanya yang belum selesai
        </label>
      </div>

      <transition-group name="fade" tag="ul" v-if="filteredActivities.length">
        <li
          v-for="(activity, index) in filteredActivities"
          :key="activity.name + index"
          :class="{ doneItem: activity.done }"
        >
          <input type="checkbox" v-model="activity.done" />
          <span :class="{ done: activity.done }">{{ activity.name }}</span>
          <button
            class="delete"
            @click="removeActivity(index)"
            title="Batalkan kegiatan"
          >
            🗑️
          </button>
        </li>
      </transition-group>
      <p v-else class="empty">✨ Tidak ada kegiatan yang ditampilkan.</p>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const activities = ref([
  { name: 'Belajar Vue.js', done: false },
  { name: 'Mengerjakan tugas', done: false },
  { name: 'Olahraga pagi', done: true },
  { name: 'Membaca buku', done: false }
])

const newActivity = ref('')
const showOnlyIncomplete = ref(false)

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

const filteredActivities = computed(() =>
  showOnlyIncomplete.value
    ? activities.value.filter(a => !a.done)
    : activities.value
)
</script>

<style scoped>
/* Background luar */
.page {
  min-height: 100vh;
  background: linear-gradient(135deg, #e0f7fa, #e3f2fd);
  display: flex;
  justify-content: center;
  align-items: flex-start;
  padding-top: 4rem;
}

/* Container dalam */
.container {
  width: 90%;
  max-width: 600px;
  background-color: #ffffff;
  border-radius: 16px;
  padding: 2rem;
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.1);
  font-family: 'Segoe UI', sans-serif;
  animation: fadeInContainer 0.8s ease;
}

@keyframes fadeInContainer {
  from {
    transform: translateY(20px);
    opacity: 0;
  }
  to {
    transform: translateY(0);
    opacity: 1;
  }
}

h1 {
  text-align: center;
  font-size: 2rem;
  color: #333;
  margin-bottom: 1.5rem;
}

.input-group {
  display: flex;
  margin-bottom: 1rem;
}

.input-group input[type="text"] {
  flex: 1;
  padding: 0.6rem 0.8rem;
  font-size: 1rem;
  border: 2px solid #ccc;
  border-radius: 8px 0 0 8px;
  outline: none;
  transition: border-color 0.2s;
}

.input-group input[type="text"]:focus {
  border-color: #42a5f5;
}

.input-group button {
  padding: 0 1rem;
  background-color: #42a5f5;
  color: white;
  border: none;
  border-radius: 0 8px 8px 0;
  cursor: pointer;
  font-size: 1.2rem;
  transition: background-color 0.3s;
}

.input-group button:hover {
  background-color: #1e88e5;
}

ul {
  list-style: none;
  padding: 0;
  margin-top: 1rem;
}

li {
  display: flex;
  align-items: center;
  background-color: #f0f4ff;
  border-radius: 8px;
  margin-bottom: 0.5rem;
  padding: 0.6rem 0.8rem;
  transition: background-color 0.3s, transform 0.2s;
}

li:hover {
  background-color: #e0ebff;
  transform: translateX(4px);
}

li input[type="checkbox"] {
  margin-right: 0.75rem;
  transform: scale(1.2);
  cursor: pointer;
}

li span {
  flex: 1;
  font-size: 1rem;
}

.done {
  text-decoration: line-through;
  color: #999;
}

.doneItem {
  opacity: 0.85;
}

.delete {
  background: none;
  border: none;
  font-size: 1.2rem;
  margin-left: 0.5rem;
  cursor: pointer;
  transition: color 0.2s;
}

.delete:hover {
  color: #d80000;
}

.filter {
  margin-top: 0.5rem;
  font-size: 0.95rem;
  color: #444;
}

.empty {
  text-align: center;
  font-style: italic;
  color: #777;
  margin-top: 1.5rem;
}

/* Transisi item */
.fade-enter-active,
.fade-leave-active {
  transition: all 0.4s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
  transform: translateY(10px);
}
</style>
