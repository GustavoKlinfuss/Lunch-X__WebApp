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
  background-color:#151515dd;
  border: solid 1px lightblue;
  color: inherit;
}

.gt-btn:hover {
  background-color:lightblue;
}

.gt-btn:focus {
  box-shadow: inherit;
  border: solid 1px lightblue;
  background-color: #151515bb;
  color:inherit;
}
</style>