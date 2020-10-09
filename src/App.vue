<template>
<main>
  <header class="header">{{header}}</header>
  <div class="container">
    <order-screen v-if="stage === StagesEnum.OrderScreen" v-on:step-completed="orderCompleted($event)"/>
    <user-info-screen v-if="stage === StagesEnum.UserInfoScreen" v-on:step-completed="userDetailsCompleted($event)"/>
  </div>
</main>
</template>

<script>
import OrderScreen from './app/order-details/OrderScreen.vue'
import UserInfoScreen from './app/user-details/UserInfoScreen.vue'
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
      order: {type: Object},
      userDetails: {type: Object}
    }
  },
  components: {
    OrderScreen,
    UserInfoScreen
  },
  methods: {
    orderCompleted: function (order) {
      this.order = order;
      this.goToNextStep();
    },
    goToNextStep: function () {
      this.stage = StagesEnum.UserInfoScreen;
    },
    userDetailsCompleted: function (userDetails) {
      this.userDetails = userDetails;
      this.finishOrder();
    },
    getPackedLunchs: function () {
      return this.order
        .filter(e => e.itemType === OrderItemTypeEnum.PackedLunch)
        .map(e => {
          return {
              size: e.size,
              meat: e.meat,
              salad: e.salad
            }
        })
    },
    getRefrigerants: function () {
      return this.order
        .filter(e => e.itemType === OrderItemTypeEnum.Refrigerant)
        .map(e => {
          return {
              type: e.itemType,
              refrigerantSize: e.refrigerantSize,
              refrigerantType: e.refrigerantType
            }
        })
    },
    finishOrder: function () {
      var orderListByItemType = {
        PackedLunch: this.getPackedLunchs(),
        Refrigerant: this.getRefrigerants()
      }

      const packedLunchMessage = this.getMessageFromPackedLunch(orderListByItemType);
      const saladMessage = this.getMessageFromSalad(orderListByItemType);
      const refrigerantMessage = this.getMessageFromRefrigerant(orderListByItemType);

      const order = `${packedLunchMessage}\n${saladMessage}\n${refrigerantMessage}`;

      // alert('Seu pedido:\n\n' + pedido);

      axios.post('http://localhost:3000/', {order})
        .then(response => console.log(response))
        .catch(error => console.log(error))
    },

    getMessageFromPackedLunch: function (orderListByItemType) {
      var message = '';
      var listened = [];

      orderListByItemType.PackedLunch.forEach(pL => {
        var packedLunchInList = listened.find(e => e.meat === pL.meat && e.size === pL.size);
        packedLunchInList 
          ? packedLunchInList.count += 1
          : listened.push({meat: pL.meat, size: pL.size, count: 1});
      })

      listened.forEach(e => {
        message += `${e.count} ${e.size} ${e.meat}\n`;
      })

      return message;
    },

    getMessageFromSalad: function (orderListByItemType) {
      var message = '';
      var listened = [];

      orderListByItemType.PackedLunch.forEach(pL => {
        var packedLunchInList = listened.find(e => e.salad === pL.salad);
        packedLunchInList 
          ? packedLunchInList.count += 1
          : listened.push({salad: pL.salad, count: 1});
      })

      listened.forEach(e => {
        message += `${e.count} Saladas ${e.salad.toLowerCase()}\n`;
      })

      return message;
    },

    getMessageFromRefrigerant: function (orderListByItemType) {
      var message = '';
      var listened = [];

      orderListByItemType.Refrigerant.forEach(refrigerant => {
        var refrigerantInList = listened.find(e => e.refrigerantType === refrigerant.refrigerantType && e.refrigerantSize === refrigerant.refrigerantSize);
        refrigerantInList 
          ? refrigerantInList.count += 1
          : listened.push({refrigerantType: refrigerant.refrigerantType, refrigerantSize: refrigerant.refrigerantSize, count: 1});
      })

      listened.forEach(e => {
        message += `${e.count} ${e.refrigerantType} ${e.refrigerantSize}\n`;
      })

      return message;
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