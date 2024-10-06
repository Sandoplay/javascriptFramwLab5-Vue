<script setup lang="ts">
import { computed } from 'vue'

interface User {
  firstName: string
  lastName: string
  gender: string
  age: number
  position: string
  photo: string
  hobbies: string[]
}

const props = defineProps<{
  user: User
}>()

const cardStyle = computed(() => ({
  backgroundColor: props.user.age < 30 ? '#2c3e50' : '#8e44ad',
  color: '#ecf0f1',
  borderColor: props.user.age < 30 ? '#3498db' : '#e74c3c'
}))
</script>

<template>
  <div class="user-card" :style="cardStyle">
    <img :src="user.photo" :alt="user.firstName + ' ' + user.lastName">
    <h2>{{ user.firstName }} {{ user.lastName }}</h2>
    <p>Gender: {{ user.gender }}</p>
    <p v-if="user.age >= 18">Age: {{ user.age }}</p>
    <p>Position: {{ user.position }}</p>
    <h3>Hobbies:</h3>
    <ul>
      <li v-for="hobby in user.hobbies" :key="hobby">{{ hobby }}</li>
    </ul>
  </div>
</template>

<style scoped>
.user-card {
  border-width: 3px;
  border-style: solid;
  border-radius: 8px;
  padding: 16px;
  margin: 16px;
  max-width: 300px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease;
}

.user-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 6px 8px rgba(0, 0, 0, 0.2);
}

.user-card img {
  width: 100%;
  border-radius: 8px;
  margin-bottom: 10px;
}

h2, h3 {
  margin-top: 0;
  color: #f39c12;
}

ul {
  padding-left: 20px;
}
</style>