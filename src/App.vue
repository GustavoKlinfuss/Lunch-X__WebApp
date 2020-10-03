<template>
  <div id="app" >
    <div class="container">
      <h1 class="header">{{header}}</h1>
      <RequestsScreen v-if="stage === 'RequestsScreen'" v-on:step-completed="completeOrder($event)"/>
      <UserInfoScreen v-if="stage === 'UserInfoScreen'" v-on:step-completed="endOrder($event)"/>
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
  },
  methods: {
    completeOrder: function (event) {
      console.log('chegou no metodo');
      console.log(event);

      this.stage = 'UserInfoScreen'
    },
    endOrder: function (event) {
      console.log(event);
      alert('pedidoFinalizado');
    }
  }
}
</script>

<style>
html, #app {
  background-color: rgb(223, 223, 223);
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  color:rgb(109, 109, 109);
  font-size: 16px;
}

.header {
	margin-top: 8px;
	padding: 12px;
	background-color: rgb(235, 235, 235);
  border: 1px solid rgb(0, 50, 107);
}

.row-div {
  display:flex;
  flex-direction: row;
}

.column-div {
  display:flex;
  flex-direction: column;
}

li {
  list-style-type: none;
}
</style>