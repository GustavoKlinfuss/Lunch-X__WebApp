<template>
<b-button size="lg" class="gt-btn my-1 border border-light" v-on:click="click()">
  <b-icon v-if="icon" :icon="icon"></b-icon>
  {{text}}
</b-button>
</template>

<script>
export default {
  props: {
    text: String,
    icon: String
  },
  methods: {
    click: function () {
      this.$emit('click');
    }
  }
}
</script>

<style scoped>
.gt-btn {
  background-color: #00326b;
}
</style>