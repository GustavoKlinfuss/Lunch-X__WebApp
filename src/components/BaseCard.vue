<template>
<div class="card pb-2 mb-2">
  <div class="p-1 d-flex justify-content-between">
    <h5 class="my-2 ml-1">
      <b-icon 
        :icon="titleIcon" 
        shift-v="2"></b-icon>
      Item {{index + 1}} - {{ cardTitle }}
    </h5>
    <b-button 
      class="align-self-center"
      variant="danger" 
      v-on:click="excludeCard()"
    >
      Remove
    </b-button>
  </div>
  <div class="ml-4">
    <slot></slot>
  </div>
</div>
</template>

<script>

export default {
  props: {
    order: Object,
    index: Number,
    titleIcon: String,
    cardTitle: String
  },

  methods: {
    excludeCard: function () {
      this.$emit('exclude-card');
		}
  }
}
</script>

<style scoped lang="scss">
.card {
  background-color: $primary;
  border: solid 2px $secondary;
  padding: 8px;
}
</style>