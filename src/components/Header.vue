<template>
  <div class="nav">
    <router-link to="/">Home</router-link>
    <router-link to="add">Add Restaurant </router-link>
    <a v-on:click="logout" href="#">Logout</a>
  </div>
</template>
<script>
export default {
  name: "Header",
  methods: {
    logout() {
      localStorage.clear();
      this.$router.push({ name: "Login" });
    },
  },
 
};
</script>

<style>
.nav {
  background-color: #333;
  overflow: hidden;
}
.nav a {
  padding: 14px 16px;
  font-size: 17px;
  float: left;
  color: #f2f2f2;
  text-decoration: none;
  margin-right: 5px;
}
.nav a:hover {
  background-color: #ddd;
  color: #333;
}
</style>
