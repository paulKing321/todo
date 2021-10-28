<template>
  <div id="nav">
    <router-link to="/">HOME</router-link> |
    <router-link to="/about">ABOUT</router-link>
  </div>
  <router-view/>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background: cadetblue;
  text-align: center;
  width: 80%;
  height: 600px;
  max-height: 600px;
  margin-left: auto;
  margin-right: auto;
  margin-top: 30px;
  box-sizing: border-box;
  box-shadow: 10px 30px  50px rgb(247, 177, 177);
  border-radius: 10px;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #fd068e;
}
</style>
