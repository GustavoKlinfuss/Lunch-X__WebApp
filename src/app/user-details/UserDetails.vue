<template>
<b-form v-on:submit="onSubmit">
  <div class="d-flex flex-column">
    <div class="card px-3 pt-2 mb-2">
      <h5>Data to contact and delivery</h5>

      <base-input 
        label="Name:" 
        v-model="userDetails.name"
        required/>

      <base-input 
        label="Street:" 
        v-model="userDetails.addressStreet"
        required/>

      <div class="d-flex">
        <base-input 
          class="w-50 mr-1"
          label="Number:" 
          v-model="userDetails.addressNumber" 
          type="number"
          required/>

        <base-input 
          class="w-50 ml-1" 
          label="Complement:" 
          v-model="userDetails.addressComplement"/>
      </div>

      <base-input  
        label="Phone:" 
        v-model="userDetails.phone"
        type="phone"
        required/>
    </div>
    <div class="d-flex">
      <base-button 
        class="back-button" 
        icon="arrow-left" 
        v-on:click="toPreviousStage()"/>
      <base-button 
        class="w-100 ml-1" 
        type="submit" 
        text="Next Stage"/>
    </div>
  </div>
</b-form>
</template>

<script>
import BaseButton from '../../components/BaseButton.vue'
import BaseInput from '../../components/BaseInput.vue'

export default {
  components: {
    BaseButton,
    BaseInput
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

    toPreviousStage: function() {
      this.$emit('to-previous-stage');
    }
  }
}
</script>

<style scoped>
.card {
  background-color:#151515;
  border: 1px solid #ff5555;
}
</style>