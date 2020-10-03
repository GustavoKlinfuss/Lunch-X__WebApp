<template>
  <div class="column-div">
    <div class="card">
    <span>Dados para contato e entrega</span><br>

    <div class="card-content">

      <!-- <GtInput :form="form" controlName="name" label="Nome:" placeholder="Seu nome aque" control="form.name"/> -->

      <b-form-group label="Nome:" label-for="name">
        <b-form-input id="name" v-model="form.name" placeholder="Seu nome aqui" trim></b-form-input>
      </b-form-group>
      <b-form-group label="Rua:" label-for="addressStreet">
        <b-form-input id="addressStreet" v-model="form.addressStreet" trim></b-form-input>
      </b-form-group>
      <div class="row-div">
        <b-form-group style="width: 49%" label="Número:" label-for="addressNumber">
          <b-form-input id="addressNumber" v-model="form.addressNumber" trim></b-form-input>
        </b-form-group>
        <b-form-group style="margin-left: 2%; width: 49%" label="Complemento:" label-for="addressComplement">
          <b-form-input id="addressComplement" v-model="form.addressComplement" trim></b-form-input>
        </b-form-group>
      </div>
      <b-form-group label="Telefone:" label-for="phone">
        <b-form-input id="phone" v-model="form.phone" trim></b-form-input>
      </b-form-group>
    </div>
    </div>
    <GtButton text="Fazer pedido" v-on:click="submitInfo()"/>

    <span>Seu nome: {{form.name}}</span>
    <span>Seu endereço: {{form.addressStreet}}, {{form.addressNumber}} - {{form.addressComplement}}</span>
    <span>Seu telefone: {{form.phone}}</span>
  </div>
</template>

<script>
import GtButton from './GtButton'

export default {
  components: {
    GtButton
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
      this.$emit('info-finished', this.form);
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