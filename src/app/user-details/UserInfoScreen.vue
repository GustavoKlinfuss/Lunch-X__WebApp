<template>
<div class="column-div">
  <b-form v-on:submit="onSubmit">
    <div class="column-div">
      <div class="card">
        <h5>Dados para contato e entrega</h5>
        <div class="card-content">
          <gt-input label="Nome:" required v-model="userDetails.name"/>
          <gt-input label="Rua:" required  v-model="userDetails.addressStreet"/>
          <div class="row-div">
            <gt-input style="width: 49%" label="Número:" required v-model="userDetails.addressNumber"/>
            <gt-input style="margin-left: 2%; width: 49%" label="Complemento:" placeholder="Opcional" v-model="userDetails.addressComplement"/>
          </div>
          <gt-input label="Telefone:" required v-model="userDetails.phone"/>
        </div>
      </div>
      <gt-button type="submit" text="Fazer pedido"/>
    </div>
  </b-form>
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
    },
    onSubmit: function(event) {
      event.preventDefault();
      this.finishUserDetails();
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