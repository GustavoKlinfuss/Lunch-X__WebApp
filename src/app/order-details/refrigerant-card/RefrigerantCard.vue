<template>
<base-card 
  titleIcon="cup-straw" 
  :index="index" 
  cardTitle="Refrigerant" 
  v-on:exclude-card="excludeCard()"
>
  <span>Option:</span>
  <base-radio 
    :options="refrigerantOptions.refrigerantTypeOptions" 
    v-model="item.refrigerantType"/>

  <span>Size:</span>
  <base-radio 
    :options="refrigerantOptions.refrigerantSizeOptions" 
    v-model="item.refrigerantSize"/>
</base-card>
</template>

<script>
import BaseRadio from '../../../components/BaseRadio.vue'
import BaseCard from '../../../components/BaseCard.vue'

export default {
  components: {
    BaseRadio,
    BaseCard
  },

  data: function () {
    return {
      refrigerantOptions: {
        refrigerantTypeOptions: ['Refrigerant 1', 'Refrigerant 2', 'Refrigerant 3', 'Refrigerant 4'],
        refrigerantSizeOptions: ['Size 1', 'Size 2', 'Size 3']
      }
    }
  },

  props: {
    item: Object,
    index: Number
  },

  methods: {
    excludeCard: function () {
      this.$emit('exclude-card', this.index)
		}
  }
}
</script>
