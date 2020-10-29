<template>
<div class="main">
  <header class="header">
    <h1>
      Make your request!
    </h1>
  </header>
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
</div>
</template>

<script>
import OrderDetails from './order-details/OrderDetails.vue'
import UserDetails from './user-details/UserDetails.vue'
import FinishOrderModal from './finish-order-modal/FinishOrderModal.vue'
import { OrderItemTypeEnum, StagesEnum } from '../variables/enums.js'
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
@import url('https://fonts.googleapis.com/css?family=Montserrat');

body {
  height: 100vh;
  display: flex;
  flex-direction: column;
}

.main {
  color: lightblue;
  font-family: Montserrat;
  font-size: 1rem;
  flex-grow: 1;
  background: repeating-linear-gradient(30deg, #bbbbbb, rgb(188, 209, 216), #bbbbbb) no-repeat;
}

.header {
	background-color: #151515dd;
  padding: 8px;
  border-bottom: 1px solid lightblue;	
  text-align: center;
  color:#bbbbbb;
  -webkit-text-stroke: 1px lightblue;
}

.fw-60 {
  width: 60px;
}
</style>