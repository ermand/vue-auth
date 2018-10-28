<template>
  <div class="w-full max-w-xs mx-auto">
    <form class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4" @submit.prevent="register">
      <div class="mb-4" v-if="errors">
        <p class="text-red text-md">{{ errors }}</p>
      </div>

      <h4 class="text-2xl text-grey-dark text-left mb-6 border-b-2 border-blue pb-2">Register</h4>

      <div class="mb-4">
        <label class="block text-grey-darker text-sm font-bold mb-2 text-left" for="first_name">
          First Name
        </label>
        <input v-model="first_name" class="shadow appearance-none border rounded w-full py-2 px-3 text-grey-darker leading-tight focus:outline-none focus:shadow-outline" id="first_name" type="text" placeholder="First Name">
      </div>

      <div class="mb-4">
        <label class="block text-grey-darker text-sm font-bold mb-2 text-left" for="last_name">
          Last Name
        </label>
        <input v-model="last_name" class="shadow appearance-none border rounded w-full py-2 px-3 text-grey-darker leading-tight focus:outline-none focus:shadow-outline" id="last_name" type="text" placeholder="Last Name">
      </div>

      <div class="mb-4">
        <label class="block text-grey-darker text-sm font-bold mb-2 text-left" for="email">
          E-mail
        </label>
        <input v-model="email" class="shadow appearance-none border rounded w-full py-2 px-3 text-grey-darker leading-tight focus:outline-none focus:shadow-outline" id="email" type="text" placeholder="E-mail">
      </div>

      <div class="mb-4">
        <label class="block text-grey-darker text-sm font-bold mb-2 text-left" for="birthday">
          Birthday
        </label>
        <input v-model="birthday" class="shadow appearance-none border rounded w-full py-2 px-3 text-grey-darker leading-tight focus:outline-none focus:shadow-outline" id="birthday" type="text" placeholder="Birthday">
      </div>

      <div class="mb-6">
        <label class="block text-grey-darker text-sm font-bold mb-2 text-left" for="password">
          Password
        </label>
        <input v-model="password" class="shadow appearance-none border rounded w-full py-2 px-3 text-grey-darker mb-3 leading-tight focus:outline-none focus:shadow-outline" id="password" type="password" placeholder="******************">
      </div>

      <div class="flex items-center justify-between">
        <button class="bg-blue hover:bg-blue-dark text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline" type="submit">
          Register
        </button>
        <a class="inline-block align-baseline font-bold text-sm text-blue hover:text-blue-darker" href="#">
          Forgot Password?
        </a>
      </div>
    </form>
    <p class="text-center text-grey text-xs">
      ©2018 Ermand Durro
    </p>
  </div>
</template>
<script>
export default {
  data() {
    return {
      first_name: "",
      last_name: "",
      birthday: "",
      email: "",
      password: ""
    };
  },
  methods: {
    register: function() {
      let data = {
        first_name: this.first_name,
        last_name: this.last_name,
        birthday: this.birthday,
        email: this.email,
        password: this.password
      };
      this.$store
        .dispatch("register", data)
        .then(() => this.$router.push("/"))
        .catch(err => console.log(err));
    }
  }
};
</script>
