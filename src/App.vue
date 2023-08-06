<script setup>
import {
  ref,
  reactive,
  computed
} from 'vue'
const data = reactive({
  isLoginForm: false,
  isRegForm: true,
  users: [],
  isloged: false,

})

const userData = reactive({
  name: '',
  username: '',
  email: '',
  password: ''
})

let notice = ref('')

function addUser() {
  if (userData.name == '' || userData.username == '' || userData.email == '' || userData.password == '') {
    notice.value = "All field is Required"
  }
  else {
    data.users.push({
      name: userData.name,
      username: userData.username,
      email: userData.email,
      password: userData.password
    })
    notice.value = "Registration successfull"
  }
}

function login() {
  if (userData.username == '' || userData.password == '') {
    notice.value = "All field is Required"
  }
  else {
    let userInfo = data.users.find((user) => {
      return (user.username === userData.username && user.password === userData.password);
    })
    if (userInfo) {
      data.isloged = true
      notice.value = ""
    }
    else
      notice.value = "Credential not match"
  }
}



</script>

<template>
  <section class="flex h-screen w-full">
    <div class="w-1/2 flex flex-col justify-center items-center"
      style="background-image: url(https://images.unsplash.com/photo-1690555575753-7aa27df96b52?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=774&q=80); background-repeat: no-repeat; background-size: cover;">
        <h1 class="text-5xl font-bold text-white">Ostad Hub!</h1>
    </div>
    <div class="w-1/2 flex flex-col justify-center items-center bg-gray-200">

      <template v-if="data.isloged == true">
        <h2 class="mb-5 text-xl">You are loged! Thank you</h2>
        <h2 class="mb-5 text-xl">Your session is started</h2>
        <button
          class="bg-orange-600 hover:bg-orange-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
          @click="data.isloged = false" type="button">
          Logout
        </button>
      </template>


      <h2 class="mb-5 text-xl" v-show="data.isloged == false">Login or register</h2>

      <h3 v-show="notice != null" class="text-red-500 mb-5">{{ notice }}</h3>
      <div class="w-full max-w-xs" v-show="data.isloged == false">
        <form class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4" @submit.prevent>
          <div class="mb-4" v-show="data.isRegForm == true">
            <label class="block text-gray-700 text-sm font-bold mb-2" for="name">
              Name
            </label>
            <input
              class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
              v-model="userData.name" id="name" type="text" placeholder="Name">
          </div>
          <div class="mb-4">
            <label class="block text-gray-700 text-sm font-bold mb-2" for="username">
              Username
            </label>
            <input
              class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
              v-model="userData.username" id="username" type="text" placeholder="Username">
          </div>
          <div class="mb-4" v-show="data.isRegForm == true">
            <label class="block text-gray-700 text-sm font-bold mb-2" for="email">
              Email
            </label>
            <input
              class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
              v-model="userData.email" id="email" type="text" placeholder="email">
          </div>
          <div class="mb-6">
            <label class="block text-gray-700 text-sm font-bold mb-2" for="password">
              Password
            </label>
            <input
              class="shadow appearance-none border  rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline"
              v-model="userData.password" id="password" type="password" placeholder="******************">
            <!-- <p class="text-red-500 text-xs italic">Please choose a password.</p> -->
          </div>



          <div class="flex items-center justify-between" v-show="data.isLoginForm == true">
            <button
              class="bg-orange-600 hover:bg-orange-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
              @click="login()" type="button">
              Sign In
            </button>
            <span class="font-bold">OR</span>
            <a class="hover:bg-orange-500  text-black font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
              @click="data.isRegForm = true,
                data.isLoginForm = false, notice = ''">
              Register
            </a>
          </div>
          <div class="flex items-center justify-between" v-show="data.isRegForm == true">
            <button
              class="bg-orange-600 hover:bg-orange-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
              @click="addUser()" type="button">
              Register
            </button>
            <span class="font-bold">OR</span>
            <a class="hover:bg-orange-500  text-black font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
              @click="data.isLoginForm = true,
                data.isRegForm = false, notice = ''">
              Sign In
            </a>
          </div>
        </form>
        <p class="text-center text-gray-500 text-xs">
          &copy;2023 <a target="_blank" class="text-orange-500" href="https://banjir-ahammad.com">Banjir Ahammad</a>. All rights reserved.
        </p>
      </div>
    </div>
  </section>
</template>
<style scoped></style>