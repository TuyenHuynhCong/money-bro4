<template>
  <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
  <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  <!-- <Game /> -->
  <CreatePlayer />
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import CreatePlayer from './components/CreatePlayer.vue'
// import Game from './components/Game.vue'
export default {
  name: 'App',
  components: {
    // HelloWorld,
    CreatePlayer,
    // Game
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
