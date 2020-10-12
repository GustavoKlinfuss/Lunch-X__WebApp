<template>
<main>
  <header class="header">{{header}}</header>
  <div class="container">
    <order-screen v-if="stage === StagesEnum.OrderScreen" v-on:step-completed="orderCompleted($event)"/>
    <user-info-screen v-if="stage === StagesEnum.UserInfoScreen" v-on:step-completed="userDetailsCompleted($event)"/>
    <finish-order-modal :showModal="showModal" :orderDetails="orderDetails" :userDetails="userDetails" v-on:modal-closed="closeModal()" v-on:order-finished="finishOrder()"/>
  </div>
</main>
</template>

<script>
import OrderScreen from './app/order-details/OrderScreen.vue'
import UserInfoScreen from './app/user-details/UserInfoScreen.vue'
import FinishOrderModal from './app/finish-order-modal/FinishOrderModal.vue'
import { OrderItemTypeEnum, StagesEnum } from './variables/enums.js'
import axios from 'axios'

export default {
  name: 'App',
  data: function () {
    return {
      stage: StagesEnum.OrderScreen,
      header: 'Tempeadori - Faça seu pedido',
      StagesEnum,
      OrderItemTypeEnum,
      orderDetails: [],
      userDetails: {type: Object},
      showModal: false
    }
  },
  components: {
    OrderScreen,
    UserInfoScreen,
    FinishOrderModal
  },
  methods: {
    closeModal: function () {
      this.showModal = false;
    },

    orderCompleted: function (order) {
      this.orderDetails = order;
      this.goToNextStep();
    },

    goToNextStep: function () {
      this.stage = StagesEnum.UserInfoScreen;
    },

    userDetailsCompleted: function (userDetails) {
      this.userDetails = userDetails;
      this.openModal();
    },

    openModal: function () {
      this.showModal = true;
    },

    finishOrder: function () {
      axios.post('http://192.168.25.188:3000/', {userDetails: this.userDetails, orderDetails: this.orderDetails})
      .then((response) => {
        if (response.data.Success) {
          alert("Seu pedido foi realizado! \n\n Será entregue em cerca de 30 minutos.");
        }
      })
      .catch(error => {
        console.log(error);
        alert('Ocorreu um erro. Por favor tente novamente!')
      })
    }
  }
}
</script>

<style>
html, main {
  background-color: rgb(223, 223, 223);
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  color:rgb(109, 109, 109);
  font-size: 16px;
}

.header {
	background-color:  rgb(0, 50, 107);
  padding: 16px 16px;
  font-size: 24px;
  color: white;
  margin-bottom: 8px;
  border-bottom: 1px solid white;
  text-align: center;
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