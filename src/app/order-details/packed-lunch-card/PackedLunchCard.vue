<template>
<div class="card">
  <div class="card-head">
    <label class="card-title"><strong>Marmita {{index + 1}}</strong></label>
    <b-button class="card-remove-button" variant="danger" v-on:click="excludeCard(index)">X</b-button>
  </div>
  
  <label class="legend-label">Opções de carne:</label>
  <GtRadio :options="packedLunchOptions.meatOptions" v-on:optionselected="selectMeat($event, order)"
    :default="packedLunchOptions.meatOptions[0]" :preselectedoption="order.meat"></GtRadio>

  <label class="legend-label">Opções de tamanho:</label>
  <GtRadio :options="packedLunchOptions.sizeOptions" v-on:optionselected="selectSize($event, order)" 
    :default="packedLunchOptions.sizeOptions[0]" :preselectedoption="order.size"></GtRadio>

  <label class="legend-label">Opções de salada:</label>
  <GtRadio :options="packedLunchOptions.saladOptions" v-on:optionselected="selectSalad($event, order)" 
    :default="packedLunchOptions.saladOptions[0]" :preselectedoption="order.salad"></GtRadio>
</div>
</template>

<script>
import GtRadio from '../../../components/GtRadio'

export default {
  name: 'RequestCard',
  components: {
    GtRadio
  },
  props: {
    order: Object,
    index: Number,
    packedLunchOptions: Object
  },
  methods: {
    selectMeat (value, order) {
			order.meat = value;
		},

		selectSize (value, order) {
			order.size = value;
		},

		selectSalad (value, order) {
			order.salad = value;
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
  border-color: rgb(0, 50, 107);
  padding-bottom: 8px;
  margin-bottom: 8px;
  border-radius: 0px;
}

.card-head {
  margin-left: 8px;
  margin-right: 8px;
	display: flex; /* Torna o elemento um flex container automaticamente transformando todos os seus filhos diretos em flex itens. */
	flex-direction: row; /* Faz com que os elementos sejam colocados todos em uma coluna, indo de cima para baixo */
	justify-content: space-between;
}

.card-title {
	font-size: 24px;
  margin-top: 8px;
  margin-left: 8px;
}

.card-remove-button {
  margin-top: 8px;;
  font-size: 14px;
  width: 40px;
  height: 40px;
  border: 1px solid rgb(0, 50, 107);
  border-radius: 0px;
}

.legend-label {
  margin: 0px 0px 0px 32px;
}
</style>