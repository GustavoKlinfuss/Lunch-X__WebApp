<template>
<main>
  <header class="header sticky-top"><h1>Tempeadori</h1></header>
  <div class="container mt-2">
    <order-screen 
      v-if="stage === StagesEnum.OrderScreen" 
      v-on:step-completed="toNextScreen()"
      :orderDetails="orderDetails"/>
    <user-info-screen 
      v-if="stage === StagesEnum.UserInfoScreen" 
      v-on:step-completed="openModal()"
      v-on:to-previous-screen="toPreviousScreen()"
      :userDetails="userDetails"/>
    <finish-order-modal 
      :orderDetails="orderDetails" 
      :userDetails="userDetails" 
      v-on:modal-closed="closeModal()" 
      v-on:order-finished="finishOrder()"/>
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
  data: function () {
    return {
      stage: StagesEnum.OrderScreen,
      StagesEnum,
      OrderItemTypeEnum,
      orderDetails: [],
      userDetails: {type: Object}
    }
  },
  components: {
    OrderScreen,
    UserInfoScreen,
    FinishOrderModal
  },
  methods: {
    toPreviousScreen: function () {
      this.stage -= 1;
    },

    toNextScreen: function () {
      this.stage += 1;
    },

    openModal: function () {
      this.$bvModal.show('finish-order-modal');
    },

    closeModal: function () {
      this.$bvModal.hide('finish-order-modal');
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
  font-size: 1rem;
}

.header {
	background-color:  #00326b;
  padding: 8px;
  color: white;
  border-bottom: 1px solid white;	
  text-align: center;
}

.back-button {
  width: 60px;
}
</style>