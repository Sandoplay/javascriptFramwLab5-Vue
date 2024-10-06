<script setup lang="ts">
import { ref, computed } from 'vue'
import UserCard from './components/UserCard.vue'

interface User {
  id: number
  firstName: string
  lastName: string
  gender: string
  age: number
  position: string
  photo: string
  hobbies: string[]
}

const users = ref<User[]>([
  { id: 1, firstName: "John", lastName: "Doe", gender: "male", age: 30, position: "Developer", photo: "https://example.com/john.jpg", hobbies: ["coding", "reading"] },
  { id: 2, firstName: "Jane", lastName: "Smith", gender: "female", age: 25, position: "Designer", photo: "https://example.com/jane.jpg", hobbies: ["drawing", "yoga"] },
  { id: 3, firstName: "Mike", lastName: "Johnson", gender: "male", age: 35, position: "Manager", photo: "https://example.com/mike.jpg", hobbies: ["golf", "cooking"] },
  { id: 4, firstName: "Emily", lastName: "Brown", gender: "female", age: 28, position: "Marketing Specialist", photo: "https://example.com/emily.jpg", hobbies: ["traveling", "photography"] },
  { id: 5, firstName: "David", lastName: "Wilson", gender: "male", age: 17, position: "CEO", photo: "https://example.com/david.jpg", hobbies: ["running", "reading"] },
  { id: 6, firstName: "Sarah", lastName: "Taylor", gender: "female", age: 32, position: "HR Manager", photo: "https://example.com/sarah.jpg", hobbies: ["yoga", "painting"] },
  { id: 7, firstName: "Chris", lastName: "Anderson", gender: "male", age: 27, position: "Sales Representative", photo: "https://example.com/chris.jpg", hobbies: ["soccer", "gaming"] },
  { id: 8, firstName: "Lisa", lastName: "Martinez", gender: "female", age: 38, position: "Project Manager", photo: "https://example.com/lisa.jpg", hobbies: ["gardening", "cooking"] },
  { id: 9, firstName: "Tom", lastName: "Garcia", gender: "male", age: 45, position: "Senior Developer", photo: "https://example.com/tom.jpg", hobbies: ["hiking", "photography"] },
  { id: 10, firstName: "Amy", lastName: "Robinson", gender: "female", age: 29, position: "Content Writer", photo: "https://example.com/amy.jpg", hobbies: ["writing", "cycling"] }
])

const genderFilter = ref('all')

const filteredUsers = computed(() => {
  if (genderFilter.value === 'all') return users.value
  return users.value.filter(user => user.gender === genderFilter.value)
})

const filterGender = (gender: string) => {
  genderFilter.value = gender
}
</script>

<template>
  <div class="app">
    <h1>User List</h1>
    <div class="toolbar">
      <button @click="filterGender('all')">All</button>
      <button @click="filterGender('male')">Male</button>
      <button @click="filterGender('female')">Female</button>
    </div>
    <div v-if="filteredUsers.length === 0">Список юзерів пустий</div>
    <div class="user-list">
      <UserCard v-for="user in filteredUsers" :key="user.id" :user="user" />
    </div>
  </div>
</template>

<style>
body {
  background-color: #1a1a1a;
  color: #ffffff;
}

.app {
  font-family: Arial, sans-serif;
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
}

.toolbar {
  margin-bottom: 20px;
}

.toolbar button {
  background-color: #4a4a4a;
  color: #ffffff;
  border: none;
  padding: 10px 15px;
  margin-right: 10px;
  cursor: pointer;
  border-radius: 5px;
}

.toolbar button:hover {
  background-color: #666666;
}

.user-list {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
}
</style>