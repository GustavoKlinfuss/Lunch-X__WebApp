<template>
<main>
  <header class="header sticky-top"><h1>Tempeadori</h1></header>
  <div class="container mt-2">
    <order-details 
      v-if="stage === StagesEnum.OrderDetails" 
      v-on:step-completed="toNextStage()"
      :orderDetails="orderDetails"/>
    <user-details
      v-if="stage === StagesEnum.UserDetails" 
      v-on:step-completed="openModal()"
      v-on:to-previous-stage="toPreviousStage()"
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
import OrderDetails from './app/order-details/OrderDetails.vue'
import UserDetails from './app/user-details/UserDetails.vue'
import FinishOrderModal from './app/finish-order-modal/FinishOrderModal.vue'
import { OrderItemTypeEnum, StagesEnum } from './variables/enums.js'
import axios from 'axios'

export default {
  components: {
    OrderDetails,
    UserDetails,
    FinishOrderModal
  },

  data: function () {
    return {
      stage: StagesEnum.OrderDetails,
      StagesEnum,
      OrderItemTypeEnum,
      orderDetails: [],
      userDetails: {type: Object}
    }
  },
  
  methods: {
    toPreviousStage: function () {
      this.stage -= 1;
    },

    toNextStage: function () {
      this.stage += 1;
    },

    openModal: function () {
      this.$bvModal.show('finish-order-modal');
    },

    closeModal: function () {
      this.$bvModal.hide('finish-order-modal');
    },

    finishOrder: function () {
      const data = {
        userDetails: this.userDetails, 
        orderDetails: this.orderDetails
      }

      axios.post('http://localhost:3000/', data)
      .then((response) => {
        if (response.data.Success) {
          alert("Your order has been placed! \n\n Will be delivered in approximately 30 minutes!");
        }
      })
      .catch(error => {
        console.log(error);
        alert('An error has ocurred. Please try again!')
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