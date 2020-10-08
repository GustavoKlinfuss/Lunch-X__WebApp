<template>
<div class="card">
  <div class="card-head">
    <label class="card-title">
      <b-icon icon="cup-straw" shift-v="2"></b-icon>
      Item {{index + 1}} - Refrigerante
    </label>
    <b-button 
      class="card-remove-button" 
      variant="danger" 
      v-on:click="excludeCard(index)">
      <b-icon 
        style="width: 20px; height: 20px;" 
        shift-v="-1" 
        shift-h="-3" 
        icon="trash"></b-icon>
      Remover refrigerante
    </b-button>
  </div>
  
  <label class="legend-label">Opção:</label>
  <GtRadio 
    :options="refrigerantOptions.refrigerantTypeOptions" 
    v-on:optionselected="selectRefrigerantType($event, order)"
    :default="refrigerantOptions.refrigerantTypeOptions[0]" 
    :preselectedoption="order.refrigerantType"></GtRadio>

  <label class="legend-label">Tamanho:</label>
  <GtRadio 
    :options="refrigerantOptions.refrigerantSizeOptions"
    v-on:optionselected="selectRefrigerantSize($event, order)" 
    :default="refrigerantOptions.refrigerantSizeOptions[0]"
    :preselectedoption="order.refrigerantSize"></GtRadio>
</div>
</template>

<script>
import GtRadio from '../../../components/GtRadio'

export default {
  name: 'RequestCard',
  components: {
    GtRadio
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
