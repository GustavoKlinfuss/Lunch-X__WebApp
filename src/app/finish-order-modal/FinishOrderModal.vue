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

    <h5>Personal information:</h5>
    <span><b>Name:</b> {{userDetails.name}}</span><br>
    <span><b>Address:</b> {{userDetails.addressStreet}}, {{userDetails.addressNumber}}</span><span v-if="userDetails.addressComplement"> - {{userDetails.addressComplement}}</span><br>
    <span><b>Phone: </b>{{userDetails.phone}}</span><br>
  </div>
  <template v-slot:modal-footer>
    <div class="d-flex w-100">
      <b-button
        class="modal-button fw-60"
        v-on:click="closeModal()"
      >
        <b-icon icon="arrow-left"></b-icon>
      </b-button>
      <b-button
        class="modal-button w-100 ml-2"
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

<style lang="scss">
.modal-button {
  background-color: transparent !important;
  border: 2px solid $secondary !important;
  color: $secondary !important;
}

.modal-button:hover {
  background-color: $primary !important;
  color: $secondary !important;
}

.modal-content {
  border: 2px solid $secondary !important;
  color: $secondary;
}

.modal-header {
  border-bottom: 1px solid $secondary !important;
}

.modal-footer {
  border-top: 1px solid $secondary !important;
}
</style>
