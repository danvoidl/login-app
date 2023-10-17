<template>
  <div class="screen">
    <Transition mode="out-in">
      <div class="container" v-if="!success">
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

        <p class="sign-up">
          Não tem uma conta? <a class="link" href="www.google.com">Cadastre-se</a>
        </p>
      </div>

      <div class="grid place-items-center gap-8" v-else>
        <p class="whitespace-pre-wrap text-center text-lg sorry">
          Desculpe! Parece que estamos offline.
        </p>
        <img src="./assets/jump.gif" alt="" class="h-[300px]" />
        <p class="text-blue-500 underline cursor-pointer go-back" @click="success = false">
          Voltar
        </p>
      </div>
    </Transition>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const user = ref({
  username: '',
  password: ''
})
const error = ref(false)
const success = ref(false)

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
  success.value = true
}
</script>

<style scoped>
.screen {
  @apply h-screen w-full grid place-items-center text-gray-600;
}
.container {
  @apply w-4/5 max-w-[420px] max-h-[500px] h-auto rounded-md m-auto my-auto p-8 grid justify-items-center gap-5;
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

.btn-save {
  @apply bg-green-400 p-2 w-full rounded-md text-white active:transform active:scale-95 transition duration-75;
}

/* we will explain what these classes do next! */
.v-enter-active,
.v-leave-active {
  transition: all 1s ease-out;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}
</style>
