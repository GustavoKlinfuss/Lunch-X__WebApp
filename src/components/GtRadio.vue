<template>
<div class="ml-4">
  <li v-for="option in options" v-bind:key="option.id">
    <b-form-radio 
      :class="selectRadioClass(option)"
      v-model="selectedValue"
      :value="option"
      v-on:change="selectOption(option)">
      {{option}}
    </b-form-radio>
  </li>
</div>
</template>

<script>
export default {
  data: function () {
    return {
        selectedValue: "",
    }
  },
  created: function () {
    if (this.preselectedoption) {
        this.selectOption(this.preselectedoption)
    } else if (this.default) {
        this.selectOption(this.default);
    }
  },
  props: {
    options: Array,
    default: String,
    preselectedoption: String
  },
  methods: {
    selectOption: function (event) {
      this.selectedValue = event;
      this.$emit('optionselected', event);
    },
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
/* .custom-control-input:checked ~ .custom-control-label::before {
  background-color:black !important;
  border-color:black !important;
} */

li {
  list-style-type: none;
}
</style>