<template>
  <div id="app" >
    <div class="container">
      <h1 class="header">{{header}}</h1>
      <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
      <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
      <RequestsScreen v-if="stage === 'RequestsScreen'"/>
      <UserInfoScreen v-if="stage === 'UserInfoScreen'"/>
    </div>
  </div>
</template>

<script>
import RequestsScreen from './components/RequestsScreen.vue'
import UserInfoScreen from './components/UserInfoScreen.vue'

export default {
  name: 'App',
  data: function () {
    return {
      stage: 'RequestsScreen',
      header: 'Tempeadori - Faça seu pedido',
    }
  },
  components: {
    RequestsScreen,
    UserInfoScreen
  }
}
</script>

<style>
html, #app {
  background-color: rgb(223, 223, 223);
}

.container {
	font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
	display: flex; /* Torna o elemento um flex container automaticamente transformando todos os seus filhos diretos em flex itens. */
	flex-direction: column; /* Faz com que os elementos sejam colocados todos em uma coluna, indo de cima para baixo */
  font-size: 20px;
  color:rgb(109, 109, 109);
}

.header {
	margin-top: 8px;
	padding: 12px;
	background-color: rgb(235, 235, 235);
	border: 1px solid rgb(0, 50, 107);
}

li {
  list-style-type: none;
}
</style>