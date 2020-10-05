<template>
<div class="column-div">
  <div class="card">
    <span>Dados para contato e entrega</span><br>

    <div class="card-content">
      <GtInput label="Nome:" placeholder="Nome" v-model="form.name"/>
      <GtInput label="Rua:" v-model="form.addressStreet"/>
      <div class="row-div">
        <GtInput style="width: 49%" label="Número:" v-model="form.addressNumber"/>
        <GtInput style="margin-left: 2%; width: 49%" label="Complemento:" v-model="form.addressComplement"/>
      </div>
      <GtInput label="Telefone:" v-model="form.phone"/>
    </div>
  </div>
  <GtButton text="Fazer pedido" v-on:click="submitInfo()"/>

  <span>Seu nome: {{form.name}}</span>
  <span>Seu endereço: {{form.addressStreet}}, {{form.addressNumber}} - {{form.addressComplement}}</span>
  <span>Seu telefone: {{form.phone}}</span>
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
      form: {
        name: '',
        addressStreet: '',
        addressNumber: '',
        addressComplement: '',
        phone: ''
      }
    }
  },
  methods: {
    submitInfo: function () {
      console.log('submitou')
      this.$emit('step-completed', this.form);
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

.form-control::-webkit-input-placeholder {
  color: #ccc;
}
</style>