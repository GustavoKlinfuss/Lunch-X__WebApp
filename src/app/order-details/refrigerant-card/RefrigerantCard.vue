<template>
<gt-card headerIcon="cup-straw" :index="index" headerText="Refrigerante" v-on:exclude-card="excludeCard()">
  <gt-label>Opção:</gt-label>
  <gt-radio :options="refrigerantOptions.refrigerantTypeOptions" v-model="item.refrigerantType"/>

  <gt-label>Tamanho:</gt-label>
  <gt-radio :options="refrigerantOptions.refrigerantSizeOptions" v-model="item.refrigerantSize"/>
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
