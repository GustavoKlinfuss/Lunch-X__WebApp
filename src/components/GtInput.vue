<template>
  <b-form-group :label="label" label-for="inp">
    <b-form-input id="inp" v-model="control" :placeholder="placeholder" trim></b-form-input>
  </b-form-group>
</template>

<script>
export default {
  props: {
    label: String,
    placeholder: String,
    controlName: String,
    form: Object,
    control: String
  },
  created: function () {
    console.log(this.controlName);

    const path = 'form.' + this.controlName;

      console.log({path});
  },
  methods: {
    getCoisa: function () {
      const path = 'form.' + this.controlName;

      console.log({path});

      return path;
    }
  }
}
</script>

<style scoped>
.form-control::-webkit-input-placeholder {
  color: #ccc;
}
</style>