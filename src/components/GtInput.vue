<template>
  <b-form-group :label="label">
    <b-form-input v-model="inputValue" :required="required" :placeholder="placeholder" trim></b-form-input>
  </b-form-group>
</template>

<script>
export default {
  props: {
    label: String,
    placeholder: String,
    value: String,
    required: Boolean
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
.form-control::-webkit-input-placeholder {
  color: #ccc;
}
</style>