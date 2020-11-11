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

<style lang="scss">
@import url('https://fonts.googleapis.com/css?family=Montserrat');
@import url('https://fonts.googleapis.com/css?family=Raleway');
@import url('https://fonts.googleapis.com/css?family=Roboto');

body {
  height: 100vh;
  display: flex;
  flex-direction: column;
}

.main {
  color: $secondary;
  font-family: 'Montserrat', sans-serif;
  font-size: 1rem;
  flex-grow: 1;
  background: linear-gradient(90deg, #151515,  #353535, #353535, #151515);
}

.header {
  font-family: 'Raleway', Roboto;
	background: $primary;
  padding: 8px;
  border-bottom: 2px solid $secondary;
  text-align: center;
  color: $secondary;
  padding: 12px 0px;
}

@media only screen and (max-device-width : 382px) {
  h1 {
    font-size: 2rem !important;
  }
}

h1 {
  margin: 0px !important;
}

.fw-60 {
  width: 60px;
}
</style>