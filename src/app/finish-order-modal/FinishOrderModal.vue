<template>
<b-modal id="finish-order-modal">
  <template v-slot:modal-header>
    <h5>Confira as informações abaixo:</h5>
  </template>
  <div class="d-block text-center">
    <h5>Informações do pedido:</h5>
    <ul>
      <li v-for="item in orderDetails" v-bind:key="item.id" class="text-left">
        <span v-if="item.itemType === OrderItemTypeEnum.PackedLunch">Marmita {{item.size}} de {{item.meat}} e Salada {{(item.salad).toLowerCase()}}<br></span>
        <span v-if="item.itemType === OrderItemTypeEnum.Refrigerant">{{item.refrigerantType}} {{item.refrigerantSize}}<br></span>
      </li>
    </ul>

    <div class="border-top border-gray mt-3 mb-2"></div>

    <h5>Informações pessoais:</h5>
    <span><strong>Nome:</strong> {{userDetails.name}}</span><br>
    <span><strong>Endereço:</strong> {{userDetails.addressStreet}}, {{userDetails.addressNumber}}</span><span v-if="userDetails.addressComplement"> - {{userDetails.addressComplement}}</span><br>
    <span><strong>Telefone: </strong>{{userDetails.phone}}</span><br>
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
        Confirmar e finalizar pedido!
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

<style scoped>
ol > li {
  list-style: linear-gradient(45, #aaaaaa, #ff0000);
}
</style>