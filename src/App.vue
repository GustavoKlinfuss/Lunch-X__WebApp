<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <RequestsScreen/>
  </div>
</template>

<script>
import RequestsScreen from './components/RequestsScreen.vue'
  // import HelloWorld from './components/HelloWorld.vue'

  export default {
    name: 'App',
    components: {
      RequestsScreen,
      // HelloWorld
    }
  }
</script>
