<template>
<div class="column-div">
  <div class="card">
    <span>Dados para contato e entrega</span><br>

    <div class="card-content">
      <GtInput label="Nome:" placeholder="Nome" v-model="userDetails.name"/>
      <GtInput label="Rua:" v-model="userDetails.addressStreet"/>
      <div class="row-div">
        <GtInput style="width: 49%" label="Número:" v-model="userDetails.addressNumber"/>
        <GtInput style="margin-left: 2%; width: 49%" label="Complemento:" v-model="userDetails.addressComplement"/>
      </div>
      <GtInput label="Telefone:" v-model="userDetails.phone"/>
    </div>
  </div>
  <GtButton text="Fazer pedido" v-on:click="finishUserDetails()"/>
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
  border-color: rgb(0, 50, 107);
  padding-bottom: 8px;
  margin-bottom: 8px;
  border-radius: 0px;
  padding: 16px;
}

.card-content {
  font-size: 14px;
}
</style>