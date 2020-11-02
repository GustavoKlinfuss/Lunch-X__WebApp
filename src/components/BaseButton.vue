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

<style scoped lang="scss">
.gt-btn {
  background-color: $primary;
  border: solid 2px $secondary;
  color: $secondary;
}

.gt-btn:hover {
  background-color: $primary;
}

.gt-btn:focus {
  box-shadow: inherit;
  border: solid 2 px $secondary;
  background-color: $primary;
}
</style>