<template>
  <div id="nav">
    <router-link to="/"><el-button style="width: 25%">Home</el-button></router-link>
    <router-link to="/about"><el-button style="width: 25%">About</el-button></router-link>
    <router-link to="/customers_path"><el-button style="width: 25%">Customers</el-button></router-link>
    <router-link to="/orders_path"><el-button style="width: 25%">Orders</el-button></router-link>
  </div>
  <router-view/>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
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
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
