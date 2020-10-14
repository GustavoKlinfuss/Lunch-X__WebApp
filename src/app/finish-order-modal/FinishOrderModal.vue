<template>
<b-modal v-model="showModal" title="">
  <template v-slot:modal-header>
      <h5>Confira as informações abaixo:</h5>
    </template>
  <div class="d-block text-center">
    <h5>Informações do pedido:</h5>
    <li v-for="(item, index) in orderDetails" v-bind:key="item.id">

      <span><strong>{{index + 1}}. </strong></span>
      <span v-if="item.itemType === OrderItemTypeEnum.PackedLunch">Marmita {{item.size}} de {{item.meat}} e salada {{(item.salad).toLowerCase()}}<br></span>
      <span v-if="item.itemType === OrderItemTypeEnum.Refrigerant">{{item.refrigerantType}} {{item.refrigerantSize}}<br></span>
    </li>

    <div class="border-top border-gray mt-3 mb-2"></div>

    <h5>Informações pessoais:</h5>
    <span><strong>Nome:</strong> {{userDetails.name}}</span><br>
    <span><strong>Endereço:</strong> {{userDetails.addressStreet}}, {{userDetails.addressNumber}}</span><span v-if="userDetails.addressComplement"> - {{userDetails.addressComplement}}</span><br>
    <span><strong>Telefone: </strong>{{userDetails.phone}}</span><br>
  </div>
  <template v-slot:modal-footer>
    <div class="d-flex">
      <b-button
        class="w-50 mr-1"
        variant="outline-warning"
        v-on:click="closeModal()"
      >
        Voltar
      </b-button>
      <b-button
        class="w-50 ml-1"
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
    showModal: Boolean,
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