<template>

  <div id="app">
    <div id="nav">
     <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <router-view />
  </div>
</template>

<style lang="scss">

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
   display: flex;
  justify-content: center;
  margin-top:0px;
  color: #2c3e50;
  background-color:  #ff9999
;
  //margin-left: 50px;
  vertical-align: middle;
  height: 700px;
}

#nav {
  margin-left:-400px;
  }
  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }

</style>
