<template>
<b-form v-on:submit="onSubmit">
  <div class="d-flex flex-column">
    <div class="card px-3 pt-2 mb-2">
      <h5>Dados para contato e entrega</h5>
      <gt-input label="Nome:" required v-model="userDetails.name"/>
      <gt-input label="Rua:" required  v-model="userDetails.addressStreet"/>
      <div class="d-flex">
        <gt-input class="w-50 mr-1" label="Número:" required v-model="userDetails.addressNumber"/>
        <gt-input class="w-50 ml-1" label="Complemento:" v-model="userDetails.addressComplement"/>
      </div>
      <gt-input type="phone" label="Telefone:" required v-model="userDetails.phone"/>
    </div>
    <div class="d-flex">
      <gt-button style="width: 60px;" icon="arrow-left" v-on:click="toPreviousScreen()"/>
      <gt-button class="w-100 ml-1" type="submit" text="Próxima etapa"/>
    </div>
  </div>
</b-form>
</template>

<script>
import GtButton from '../../components/GtButton.vue'
import GtInput from '../../components/GtInput.vue'

export default {
  components: {
    GtButton,
    GtInput
  },
  props: {
    userDetails: {
      name: String,
      addressStreet: String,
      addressNumber: String,
      addressComplement: String,
      phone: String
    }
  },
  methods: {
    finishUserDetails: function () {
      this.$emit('step-completed', this.userDetails);
    },

    onSubmit: function(event) {
      event.preventDefault();
      this.finishUserDetails();
    },

    toPreviousScreen: function() {
      this.$emit('to-previous-screen');
    }
  }
}
</script>

<style scoped>
.card {
  background-color:#ebebeb;
}
</style>