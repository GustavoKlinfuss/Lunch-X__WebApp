<template>
<div class="gtRadioButtonGroup">
    <li v-for="option in options" v-bind:key="option.id">
        <b-form-radio :class="thisOptionSelected(option)? radioSelected(): radioNotSelected()" button-variant="warning" size="lg" v-model="selectedValue" :value="option" v-on:change="selectOption(option)">{{option}}</b-form-radio>
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
        selectOption (event) {
            this.selectedValue = event;
            this.$emit('optionselected', event);
        },
        thisOptionSelected(value) {
            return value === this.selectedValue;
        },
        radioSelected() { return 'radio-selected gtRadioButton'; },
        radioNotSelected() { return 'radio-not-selected gtRadioButton'; }
    },
};
</script>

<style>
.radio-selected {
  color: rgb(66, 66, 66);
  font-weight: bolder !important;
}

.radio-not-selected {
  color: gray;
}

.gtRadioButtonGroup {
    margin-left: 64px;
}

.gtRadioButton {
    margin-top: 8px;
}

.custom-control-input:checked ~ .custom-control-label::before {
    background-color: black !important;
    border-color: black !important;
}

</style>