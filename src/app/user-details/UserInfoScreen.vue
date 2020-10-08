<template>
<div class="column-div">
  <div class="card">
    <label>Dados para contato e entrega</label><br>

    <div class="card-content">
      <gt-input label="Nome:" placeholder="Nome" v-model="userDetails.name"/>
      <gt-input label="Rua:" v-model="userDetails.addressStreet"/>
      <div class="row-div">
        <gt-input style="width: 49%" label="Número:" v-model="userDetails.addressNumber"/>
        <gt-input style="margin-left: 2%; width: 49%" label="Complemento:" v-model="userDetails.addressComplement"/>
      </div>
      <gt-input label="Telefone:" v-model="userDetails.phone"/>
    </div>
  </div>
  <gt-button text="Fazer pedido" v-on:click="finishUserDetails()"/>
</div>
</template>

<script>
import GtButton from '../../components/GtButton.vue'
import GtInput from '../../components/GtInput.vue'

export default {
  components: {
    GtButton,
    GtInput
  },
  data: function () {
    return {
      userDetails: {
        name: '',
        addressStreet: '',
        addressNumber: '',
        addressComplement: '',
        phone: ''
      }
    }
  },
  methods: {
    finishUserDetails: function () {
      this.$emit('step-completed', this.userDetails);
    }
  }
  
}
</script>

<style scoped>
.card {
  background-color: rgb(235, 235, 235);
  padding-bottom: 8px;
  margin-bottom: 8px;
  padding: 16px;
}

.card-content {
  font-size: 14px;
}
</style>