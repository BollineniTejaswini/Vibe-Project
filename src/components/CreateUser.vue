<script setup lang="ts">
import { ref } from 'vue'

interface User {
  name: string
  email: string
}

const user = ref<User>({ name: '', email: '' })
const submitted = ref(false)

const emit = defineEmits(['user-created'])

function submitForm() {
  submitted.value = true
  emit('user-created', { ...user.value })
}
function resetForm() {
  user.value = { name: '', email: '' }
  submitted.value = false
}
</script>

<template>
  <form @submit.prevent="submitForm" v-if="!submitted" class="modern-form">
    <div class="form-group">
      <label for="name">Name</label>
      <input id="name" v-model="user.name" type="text" required placeholder="Enter your name" />
    </div>
    <div class="form-group">
      <label for="email">Email</label>
      <input id="email" v-model="user.email" type="email" required placeholder="Enter your email" />
    </div>
    <button class="primary" type="submit">Create Account</button>
  </form>
  <div v-else class="success-message">
    <h3>Welcome, {{ user.name }}!</h3>
    <p>Your account has been created.</p>
    <button class="secondary" @click="resetForm">Create Another</button>
  </div>
</template>

<style scoped>
.modern-form {
  display: flex;
  flex-direction: column;
  gap: 1.5em;
  background: #fff;
  border-radius: 16px;
  box-shadow: 0 4px 24px rgba(60, 60, 120, 0.08);
  padding: 2em 1.5em;
  min-width: 260px;
}
.form-group {
  display: flex;
  flex-direction: column;
  gap: 0.5em;
}
label {
  font-weight: 600;
  color: #6366f1;
}
input {
  padding: 0.75em;
  border: 1px solid #d1d5db;
  border-radius: 8px;
  font-size: 1em;
  outline: none;
  transition: border 0.2s;
}
input:focus {
  border: 1.5px solid #6366f1;
}
.primary {
  background: linear-gradient(90deg, #6366f1 0%, #42b883 100%);
  color: #fff;
  border: none;
  border-radius: 8px;
  padding: 0.75em 2em;
  font-size: 1em;
  cursor: pointer;
  margin-top: 1em;
  box-shadow: 0 2px 8px rgba(60, 60, 120, 0.08);
  transition: background 0.2s;
}
.primary:hover {
  background: linear-gradient(90deg, #42b883 0%, #6366f1 100%);
}
.success-message {
  text-align: center;
  background: #f0fdf4;
  border-radius: 16px;
  padding: 2em 1.5em;
  box-shadow: 0 2px 8px rgba(60, 60, 120, 0.08);
}
.secondary {
  background: #fff;
  color: #6366f1;
  border: 1.5px solid #6366f1;
  border-radius: 8px;
  padding: 0.5em 1.5em;
  font-size: 1em;
  margin-top: 1.5em;
  cursor: pointer;
  transition: background 0.2s, color 0.2s;
}
.secondary:hover {
  background: #6366f1;
  color: #fff;
}
</style>
