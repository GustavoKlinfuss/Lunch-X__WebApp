<template>
<b-button
  size="lg"
  class="gt-btn my-1"
  v-on:click="click()"
>
  <b-icon
    v-if="icon"
    :icon="icon"/>
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
  background-color: #111111;
  border: solid 1px  #ff5555;
  color: #ff5555;
}
</style>