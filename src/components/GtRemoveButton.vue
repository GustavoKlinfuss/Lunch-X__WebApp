<template>
<b-button 
  class="mt-2" 
  variant="danger" 
  v-on:click="click()"
  >
  <b-icon icon="trash"></b-icon>
  <span>Remover</span>
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