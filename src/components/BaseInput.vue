<template>
  <b-form-group :label="label">
    <b-form-input v-if="type === 'phone'" type="tel" v-model="inputValue" :required="required" v-mask="['(##) ####-####', '(##) #####-####']" :placeholder="placeholder" trim></b-form-input>
    <b-form-input v-else-if="type" :type="type" v-model="inputValue" :required="required" :placeholder="placeholder" trim></b-form-input>
    <b-form-input v-else v-model="inputValue" :required="required" :placeholder="placeholder" trim></b-form-input>
  </b-form-group>
</template>

<script>
import {mask} from 'vue-the-mask'

export default {
  directives: {mask},
  props: {
    label: String,
    placeholder: String,
    value: String,
    required: Boolean,
    type: String
  },
  computed: {
    inputValue: {
      get: function () {
        return this.value;
      },
      set: function (val) {
        this.$emit('input', val);
      }
    }
  }
}
</script>

<style scoped>
.form-control {
  background-color: #24292E;
  color: #ff5555;
}
</style>