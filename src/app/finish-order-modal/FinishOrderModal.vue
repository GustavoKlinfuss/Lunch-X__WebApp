<template>
<b-modal v-model="showModal" title="">
  <template v-slot:modal-header>
      <h5>Confira as informações abaixo:</h5>
    </template>
  <div class="d-block text-center">
    <h5>Informações do pedido:</h5>
    <li v-for="(item, index) in orderDetails" v-bind:key="item.id">

      <span><strong>{{index + 1}}. </strong></span>
      <span v-if="item.itemType === OrderItemTypeEnum.PackedLunch">Marmita {{item.size}} de {{item.meat}}<br></span>
      <span v-if="item.itemType === OrderItemTypeEnum.Refrigerant">{{item.refrigerantType}} {{item.refrigerantSize}}<br></span>
    </li>

    <div style="border-top: 1px solid #dee2e6; margin-top: 20px; margin-bottom: 10px;"></div>

    <h5>Informações pessoais:</h5>
    <span><strong>Nome:</strong> {{userDetails.name}}</span><br>
    <span><strong>Endereço:</strong> {{userDetails.addressStreet}}, {{userDetails.addressNumber}}</span><span v-if="userDetails.addressComplement"> - {{userDetails.addressComplement}}</span><br>
    <span><strong>Telefone: </strong>{{userDetails.phone}}</span><br>
  </div>
  <template v-slot:modal-footer>
    <div style="width: 100%; display: flex; justify-content: space-between;">
      <b-button
        style="width: 49%"
        variant="outline-warning"
        v-on:click="closeModal()"
      >
        Voltar
      </b-button>
      <b-button
        style="width: 49%"
        variant="outline-success"
        v-on:click="finishOrder()"
      >
        Confirmar e finalizar pedido!
      </b-button>
    </div>
  </template>
  <!-- <b-button class="mt-2" variant="outline-success" block @click="consolalogai(1)">Confirmar e fazer pedido</b-button> -->
  <!-- <b-button class="mt-2" variant="outline-warning" block @click="consolalogai(2)">Voltar</b-button> -->
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