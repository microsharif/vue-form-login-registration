<script setup>
  import Register from './components/Register.vue'
  import Login from './components/Login.vue'
  import { ref, reactive, computed } from 'vue'

  const registerSuccess = ref(false)
  const loginSucess = ref(false)
  const loginRegisterTxt = ref('')
  const titleText = ref('Register')
  const registerData = reactive({
    email: '',
    password: '',
    confirmpassword:'',
  })

  const updateRgisterStatus = (status) => {
    registerSuccess.value = status
    loginRegisterTxt.value = "Successfully Register"
    titleText.value = 'Login'
  }
  
  const updateLoginStatus = (status) => {
    loginSucess.value = status
  }
</script>

<template>
  <section class="flex h-screen w-full">
    <template v-if="!loginSucess">
      <div class="w-1/2" style="background-image: url(https://images.unsplash.com/photo-1690555575753-7aa27df96b52?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=774&q=80); background-repeat: no-repeat; background-size: cover;">
        <h1 class="mb-5 text-2xl mt-10 ml-10 text-white">Kosmos!</h1>
      </div>
      <div class="w-1/2 flex flex-col justify-center items-center bg-gray-200">
        <h2 class="mb-5 text-xl">{{ titleText }}</h2>
        <p v-show="registerSuccess && loginRegisterTxt" class="text-green-500 text-xs italic mb-3">{{ loginRegisterTxt }}</p>
        <div class="w-full max-w-xs">
          <Register v-if="!registerSuccess" @updateRgisterStatus = "updateRgisterStatus" :registerData = "registerData"></Register>
          <Login @updateLoginStatus = "updateLoginStatus" v-else></Login>

          <p v-if="titleText == 'Register' " class="text-black-500 text-xs italic mb-3 mt-3 text-center">Already have a account <span class="cursor-pointer text-blue-500 font-bold" @click.prevent="registerSuccess = true; titleText = 'Login'">Sign In</span></p>

          <p v-if="titleText == 'Login' " class="text-black-500 text-xs italic mb-3 mt-3 text-center">Don't have a account <span class="cursor-pointer text-blue-500 font-bold" @click.prevent="registerSuccess = false; titleText = 'Register'">Register</span></p>
          <p class="text-center text-gray-500 text-xs">
            &copy;2020 Acme Corp. All rights reserved.
          </p>
        </div>
      </div>
    </template>
    <template v-else>
      <div class="w-full" style="background-image: url(https://images.unsplash.com/photo-1690555575753-7aa27df96b52?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=774&q=80); background-repeat: no-repeat; background-size: cover;">
        <h1 class="mb-5 text-2xl mt-10 text-white text-center">Welocome</h1>
        <p class="text-green-500 text-xs italic mb-3 text-center">Successfully Loged In</p>
      </div>
    </template>
  </section>
</template>
<style scoped></style>
