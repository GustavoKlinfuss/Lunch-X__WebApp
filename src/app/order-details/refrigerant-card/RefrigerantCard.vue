<template>
<div class="card">
  <div class="card-head">
    <label class="card-title"><strong>Item {{index + 1}} - Refrigerante</strong></label>
    <b-button class="card-remove-button" variant="danger" v-on:click="excludeCard(index)">X</b-button>
  </div>
  
  <label class="legend-label">Opção:</label>
  <GtRadio :options="refrigerantOptions.refrigerantTypeOptions" v-on:optionselected="selectRefrigerantType($event, order)"
    :default="refrigerantOptions.refrigerantTypeOptions[0]" :preselectedoption="order.refrigerantType"></GtRadio>
  <label class="legend-label">Tamanho:</label>
  <GtRadio :options="refrigerantOptions.refrigerantSizeOptions" v-on:optionselected="selectRefrigerantSize($event, order)" 
    :default="refrigerantOptions.refrigerantSizeOptions[0]" :preselectedoption="order.refrigerantSize"></GtRadio>
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
    refrigerantOptions: Object
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