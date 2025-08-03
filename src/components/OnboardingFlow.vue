<script setup lang="ts">
import { ref } from 'vue'
import CreateUser from './CreateUser.vue'

const step = ref(1)
const userCreated = ref(false)

function nextStep() {
  step.value++
}
function onUserCreated() {
  userCreated.value = true
  nextStep()
}
function restart() {
  step.value = 1
  userCreated.value = false
}
</script>

<template>
  <div class="onboarding-container">
    <transition name="fade" mode="out-in">
      <div v-if="step === 1" key="welcome" class="onboarding-step">
        <h2>Welcome to Vibe!</h2>
        <p>Let's get you started with a quick onboarding.</p>
        <button class="primary" @click="nextStep">Start</button>
      </div>
      <div v-else-if="step === 2" key="create-user" class="onboarding-step">
        <h2>Create Your Account</h2>
        <CreateUser @user-created="onUserCreated" />
      </div>
      <div v-else-if="step === 3" key="success" class="onboarding-step">
        <h2>You're All Set!</h2>
        <p>Your account has been created. Enjoy using Vibe!</p>
        <button class="primary" @click="restart">Restart Onboarding</button>
      </div>
    </transition>
  </div>
</template>

<style scoped>
.onboarding-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-height: 60vh;
  background: linear-gradient(135deg, #f8fafc 0%, #e0e7ff 100%);
  border-radius: 24px;
  box-shadow: 0 8px 32px rgba(60, 60, 120, 0.08);
  padding: 2.5em 2em;
  max-width: 400px;
  margin: 2em auto;
}
.onboarding-step {
  display: flex;
  flex-direction: column;
  align-items: center;
  animation: fadeIn 0.5s;
}
.primary {
  background: linear-gradient(90deg, #6366f1 0%, #42b883 100%);
  color: #fff;
  border: none;
  border-radius: 8px;
  padding: 0.75em 2em;
  font-size: 1.1em;
  margin-top: 2em;
  cursor: pointer;
  box-shadow: 0 2px 8px rgba(60, 60, 120, 0.08);
  transition: background 0.2s;
}
.primary:hover {
  background: linear-gradient(90deg, #42b883 0%, #6366f1 100%);
}
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.4s;
}
.fade-enter-from, .fade-leave-to {
  opacity: 0;
}
@keyframes fadeIn {
  from { opacity: 0; transform: translateY(20px); }
  to { opacity: 1; transform: translateY(0); }
}
</style>
