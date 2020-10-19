<template>
<gt-card 
  titleIcon="cup-straw" 
  :index="index" 
  cardTitle="Refrigerant" 
  v-on:exclude-card="excludeCard()"
>
  <span>Option:</span>
  <gt-radio 
    :options="refrigerantOptions.refrigerantTypeOptions" 
    v-model="item.refrigerantType"/>

  <span>Size:</span>
  <gt-radio 
    :options="refrigerantOptions.refrigerantSizeOptions" 
    v-model="item.refrigerantSize"/>
</gt-card>
</template>

<script>
import GtRadio from '../../../components/GtRadio.vue'
import GtCard from '../../../components/GtCard.vue'

export default {
  components: {
    GtRadio,
    GtCard
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
