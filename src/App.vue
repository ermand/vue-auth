<template>
  <div id="app" class="bg-grey-light h-screen">
    <div id="nav">
      <router-link to="/" class="mx-4">Home</router-link>
      <router-link to="/about" class="mx-4">About</router-link>
      <template v-if="isLoggedIn">
        <router-link to="/account" class="mx-4">Account</router-link>
        <span class="mx-4"><a @click="logout">Logout</a></span>
      </template>
      <template v-else>
        <router-link to="/register" class="mx-4">Register</router-link>
        <router-link to="/login" class="mx-4">Login</router-link>
      </template>
    </div>
    <router-view/>
  </div>
</template>

<script>
export default {
  computed: {
    isLoggedIn: function() {
      return this.$store.getters.isLoggedIn;
    }
  },
  methods: {
    logout: function() {
      this.$store.dispatch("logout").then(() => {
        this.$router.push("/login");
      });
    }
  },
  created() {
    this.$http.interceptors.response.use(undefined, function(err) {
      return new Promise(function(resolve, reject) {
        if (err.status === 401 && err.config && !err.config.__isRetryRequest) {
          this.$store.dispatch("logout");
        }

        reject(err);
        throw err;
      });
    });
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#nav {
  padding: 30px;
}
#nav a {
  font-weight: bold;
  color: #2c3e50;
  cursor: pointer;
}
#nav a:hover {
  text-decoration: underline;
}
#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
