<template>
<div class="card pb-2 mb-2">
  <div class="p-1 d-flex justify-content-between">
    <h5 class="my-2 ml-1">
      <b-icon :icon="headerIcon" shift-v="2"></b-icon>
      Item {{index + 1}} - {{ headerText }}
    </h5>
    <gt-remove-button v-on:click="excludeCard()"/>
  </div>
  <div class="ml-4">
    <slot></slot>
  </div>
</div>
</template>

<script>
import GtRemoveButton from '../components/GtRemoveButton.vue'

export default {
  components: {
    GtRemoveButton
  },
  
  props: {
    order: Object,
    index: Number,
    headerIcon: String,
    headerText: String
  },
  methods: {
    excludeCard: function () {
      this.$emit('exclude-card');
		}
  }
}
</script>

<style scoped>
.card {
  background-color: #ebebeb;
}
</style>