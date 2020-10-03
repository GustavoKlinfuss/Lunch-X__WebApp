<template>
<div class="gtRadioButtonGroup">
  <li v-for="option in options" v-bind:key="option.id">
    <b-form-radio :class="selectRadioClass(option)" button-variant="warning"
      v-model="selectedValue" :value="option" v-on:change="selectOption(option)">
      {{option}}
    </b-form-radio>
  </li>
</div>
</template>

<script>
export default {
  name: 'GtRadio',
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
      const classOfRadio = option === this.selectedValue
        ? 'radio-selected gtRadioButton'
        : 'gtRadioButton';

      return classOfRadio;
    }
  }
};
</script>

<style>
.radio-selected {
  font-weight: bolder !important;
}

.gtRadioButtonGroup {
    margin-left: 64px;
}

.gtRadioButton {
    margin-top: 8px;
}

.custom-control-input:checked ~ .custom-control-label::before {
    background-color: rgb(0, 50, 107) !important;
    border-color: rgb(0, 50, 107) !important;
}

</style>