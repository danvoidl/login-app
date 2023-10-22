<template>
  <div class="my-auto block">
    <div class="container">
      <p class="title">Bem-vindo!</p>
  
      <div class="w-full">
        <label for="username" class="block user">Usuário</label>
        <input v-model="user.username" type="text" class="username" />
      </div>
  
      <div class="w-full">
        <label for="password" class="block pass">Senha</label>
        <input v-model="user.password" type="password" class="password" />
      </div>
  
      <p v-show="error" class="text-red-600">Usuário ou senha incorretos!</p>
  
      <a class="justify-self-end link forgot">Esqueci minha senha</a>
  
      <button class="btn-save" @click="login">Entrar</button>
  
      <p class="sign-up">Não tem uma conta? <a class="link" href="www.google.com">Cadastre-se</a></p>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()
const error = ref(false)
const user = ref({
  username: '',
  password: ''
})

const login = () => {
  error.value = false
  const username = 'admin'
  const password = '123456789'

  if (user.value.password !== password || user.value.username !== username) {
    error.value = true
    return
  }

  user.value = {
    password: '',
    username: ''
  }

  router.push({ path: '/student-registers' })
}
</script>

<style scoped>
.container {
  @apply w-4/5 max-w-[420px] max-h-[500px] h-auto rounded-md m-auto p-8 grid justify-items-center gap-5;
}

.btn-save {
  @apply bg-green-400 p-2 w-full rounded-md text-white active:transform active:scale-95 transition duration-75;
}

.title {
  @apply text-gray-600 text-2xl;
}

input {
  @apply outline-none p-2 rounded-md focus:outline-green-500 w-full outline-2 outline-gray-200;
}

.link {
  @apply underline text-blue-500;
}
</style>
