<template>
<label>
  <span>
    {{text}}
  </span>
</label>
</template>

<script>

export default {
  props: {
    text: String
  },
}
</script>

<style scoped>
label {
  margin: 0px;
}
</style>