<template>
<b-button size="lg" class="gt-btn" v-on:click="click()">
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
	margin: 4px 0px 4px 0px;
  background-color:  rgb(0, 50, 107);
  border: 1px solid white;
}
</style>