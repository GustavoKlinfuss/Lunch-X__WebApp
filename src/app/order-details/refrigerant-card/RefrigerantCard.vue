<template>
<div class="card">
  <div class="card-head">
    <h5 class="card-title">
      <b-icon icon="cup-straw" shift-v="2"></b-icon>
      Item {{index + 1}} - Refrigerante
    </h5>
    <b-button 
      class="card-remove-button" 
      variant="danger" 
      v-on:click="excludeCard(index)">
      <b-icon icon="trash"></b-icon>
      <span>Remover</span>
    </b-button>
  </div>
  <div class="card-content">
    <gt-label text="Opção:"/>
    <GtRadio 
      :options="refrigerantOptions.refrigerantTypeOptions" 
      v-on:optionselected="selectRefrigerantType($event, order)"
      :default="refrigerantOptions.refrigerantTypeOptions[0]" 
      :preselectedoption="order.refrigerantType"></GtRadio>

    <gt-label text="Tamanho:"/>
    <GtRadio 
      :options="refrigerantOptions.refrigerantSizeOptions"
      v-on:optionselected="selectRefrigerantSize($event, order)" 
      :default="refrigerantOptions.refrigerantSizeOptions[0]"
      :preselectedoption="order.refrigerantSize"></GtRadio>
  </div>
</div>
</template>

<script>
import GtRadio from '../../../components/GtRadio.vue'
import GtLabel from '../../../components/GtLabel.vue'

export default {
  name: 'RequestCard',
  components: {
    GtRadio,
    GtLabel
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
    order: Object,
    index: Number
  },
  methods: {
    selectRefrigerantType (value, order) {
			order.refrigerantType = value;
		},

		selectRefrigerantSize (value, order) {
			order.refrigerantSize = value;
		},

    excludeCard: function () {
      this.$emit('card-excluded', this.index)
		}
  }
}
</script>
