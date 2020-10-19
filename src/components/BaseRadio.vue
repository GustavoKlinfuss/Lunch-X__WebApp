<template>
<div class="ml-4">
  <li 
    class="radio-li"
    v-for="option in options" 
    v-bind:key="option.id"
  >
    <b-form-radio 
      :class="selectRadioClass(option)"
      v-model="selectedValue"
      :value="option"
    >
      {{option}}
    </b-form-radio>
  </li>
</div>
</template>

<script>
export default {
  created: function () {
    if (!this.value) {
      this.selectedValue = this.options[0];
    }
  },
  props: {
    options: Array,
    default: String,
    value: String
  },
  computed: {
    selectedValue: {
      get: function () {
        return this.value;
      },
      set: function (val) {
        this.$emit('input', val);
      }
    }
  },
  methods: {
    selectRadioClass : function (option) {
      const radioClass = option === this.selectedValue
        ? 'font-weight-bold my-1'
        : 'my-1';

      return radioClass;
    }
  }
};
</script>

<style>
.custom-control-input:checked ~ .custom-control-label::before {
  background-color:#ff5555 !important;
  border-color: #ff5555 !important;
}

.custom-control-label::before {
  background-color: #24292E !important;
  border-color: #ff5555 !important;
}

.radio-li {
  list-style-type: none;
}
</style>