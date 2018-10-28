<template>
  <div class="w-full max-w-xs mx-auto">
    <form class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4" @submit.prevent="login">
      <div class="mb-4" v-if="errors">
        <p class="text-red text-md">{{ errors }}</p>
      </div>

      <div class="mb-4">
        <label class="block text-grey-darker text-sm font-bold mb-2" for="username">
          E-mail
        </label>
        <input v-model="email" class="shadow appearance-none border rounded w-full py-2 px-3 text-grey-darker leading-tight focus:outline-none focus:shadow-outline" id="email" type="text" placeholder="E-mail">
      </div>
      <div class="mb-6">
        <label class="block text-grey-darker text-sm font-bold mb-2" for="password">
          Password
        </label>
        <input v-model="password" class="shadow appearance-none border border-red rounded w-full py-2 px-3 text-grey-darker mb-3 leading-tight focus:outline-none focus:shadow-outline" id="password" type="password" placeholder="******************">
        <p class="text-red text-xs italic">Please choose a password.</p>
      </div>
      <div class="flex items-center justify-between">
        <button class="bg-blue hover:bg-blue-dark text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline" type="submit">
          Sign In
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
      email: "",
      password: "",
      errors: null
    };
  },
  methods: {
    login: function() {
      let email = this.email;
      let password = this.password;
      this.$store
        .dispatch("login", { email, password })
        .then(() => this.$router.push("/"))
        .catch(err => (this.errors = err));
    }
  }
};
</script>
