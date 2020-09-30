<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <Main/>
  </div>
</template>

<script>
import Main from './components/Main.vue'
  // import HelloWorld from './components/HelloWorld.vue'

  export default {
    name: 'App',
    components: {
      Main,
      // HelloWorld
    }
  }
</script>
