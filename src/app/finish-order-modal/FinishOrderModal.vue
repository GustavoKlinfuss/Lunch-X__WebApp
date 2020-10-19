<template>
<b-modal id="finish-order-modal">
  <template v-slot:modal-header>
    <h5>Check out the information below:</h5>
  </template>
  <div class="d-block text-center">
    <h5>Order information:</h5>
    <ul>
      <li 
        v-for="item in orderDetails" 
        v-bind:key="item.id" 
        class="text-left"
      >
        <span v-if="item.itemType === OrderItemTypeEnum.PackedLunch">{{item.size}} packed lunch of {{item.meat}} and salad {{(item.salad).toLowerCase()}}<br></span>
        <span v-if="item.itemType === OrderItemTypeEnum.Refrigerant">{{item.refrigerantType}} - {{item.refrigerantSize}}<br></span>
      </li>
    </ul>

    <hr>

    <h5>Personal information:</h5>
    <span><b>Name:</b> {{userDetails.name}}</span><br>
    <span><b>Address:</b> {{userDetails.addressStreet}}, {{userDetails.addressNumber}}</span><span v-if="userDetails.addressComplement"> - {{userDetails.addressComplement}}</span><br>
    <span><b>Phone: </b>{{userDetails.phone}}</span><br>
  </div>
  <template v-slot:modal-footer>
    <div class="d-flex w-100">
      <b-button
        class="back-button"
        variant="outline-warning"
        v-on:click="closeModal()"
      >
        <b-icon icon="arrow-left"></b-icon>
      </b-button>
      <b-button
        class="w-100 ml-2"
        variant="outline-success"
        v-on:click="finishOrder()"
      >
        Confirm and finalize order!
      </b-button>
    </div>
  </template>
</b-modal>
</template>

<script>
import { OrderItemTypeEnum } from '../../variables/enums.js'

export default {
  data: function () {
    return { OrderItemTypeEnum }
  },

  props: {
    orderDetails: Array,
    userDetails: Object
  },
  
  methods: {
    closeModal: function() {
      this.$emit('modal-closed');
    },
    finishOrder: function() {
      this.$emit('order-finished');
    }
  }
}
</script>

<style>
.modal-header {
  border-bottom: 1px solid rgba(0, 0, 0, 0.1);;
}
.modal-content {
  background-color: #24292E !important;
  border: 1px solid #ff5555;
  color:  #ff5555;
}
.modal-footer {
  border-top: 1px solid rgba(0, 0, 0, 0.1);;
}
</style>
