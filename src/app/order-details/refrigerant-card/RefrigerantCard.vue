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
      X
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

<style scoped>
.card {
  background-color: rgb(235, 235, 235);
  padding-bottom: 8px;
  margin-bottom: 8px;
}

.card-head {
  margin-left: 8px;
  margin-right: 8px;
	display: flex;
	flex-direction: row;
	justify-content: space-between;
}

.card-title {
	font-size: 24px;
  margin-top: 8px;
  margin-left: 8px;
  font-weight: bolder;
}

.card-remove-button {
  margin-top: 8px;;
  font-size: 14px;
  width: 40px;
  height: 40px;
}

.legend-label {
  margin: 0px 0px 0px 32px;
}
</style>