<template>
<gt-card headerIcon="cup-straw" :index="index" headerText="Refrigerante" v-on:exclude-card="excludeCard()">
  <gt-label text="Opção:"/>
  <GtRadio 
    :options="refrigerantOptions.refrigerantTypeOptions" 
    v-on:optionselected="item.refrigerantType = $event"
    :default="refrigerantOptions.refrigerantTypeOptions[0]" 
    :preselectedoption="item.refrigerantType"></GtRadio>

  <gt-label text="Tamanho:"/>
  <GtRadio 
    :options="refrigerantOptions.refrigerantSizeOptions"
    v-on:optionselected="item.refrigerantSize = $event" 
    :default="refrigerantOptions.refrigerantSizeOptions[0]"
    :preselectedoption="item.refrigerantSize"></GtRadio>
</gt-card>
</template>

<script>
import GtRadio from '../../../components/GtRadio.vue'
import GtLabel from '../../../components/GtLabel.vue'
import GtCard from '../../../components/GtCard.vue'

export default {
  name: 'RequestCard',
  components: {
    GtRadio,
    GtLabel,
    GtCard
  },
  data: function () {
    return {
      refrigerantOptions: {
        refrigerantTypeOptions: ['Coca-cola', 'Fanta laranja', 'Sprite', 'Guaraná Kuat'],
        refrigerantSizeOptions: ['300ml', '600ml', '1 litro', '2 litros']
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
