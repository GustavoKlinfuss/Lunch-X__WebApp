<template>
<b-button 
  class="align-self-center"
  variant="danger" 
  v-on:click="click()"
  >
  <div class="d-flex aligh-items-center">
    <!-- <b-icon icon="trash" shift-v="-2" shift-h="-3"></b-icon> -->
    <span>Remover</span>
  </div>
</b-button>
</template>

<script>
export default {
  methods: {
    click() {
      this.$emit('click');
    }
  }
}
</script>

<style scoped>
/* .remove-button { */
  /* height: 40px; */
/* } */
</style>