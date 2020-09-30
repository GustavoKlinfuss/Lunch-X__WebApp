<template>
  <div class="card">
    <div class="cardHead">
      <label class="cardTitle"><strong>Marmita {{index + 1}}</strong></label>
      <b-button class="cardRemoveButton" variant="danger" @click="excludeCard(index)">X</b-button>
    </div>
    
    <label class="legendLabel">Opções de carne:</label>
    <GtRadio :options="requestOptions.meatOptions" @optionselected="selectMeat($event, request)"
      :default="requestOptions.meatOptions[0]" :preselectedoption="request.meat"></GtRadio>

    <label class="legendLabel">Opções de tamanho:</label>
    <GtRadio :options="requestOptions.sizeOptions" @optionselected="selectSize($event, request)" 
      :default="requestOptions.sizeOptions[0]" :preselectedoption="request.size"></GtRadio>

    <label class="legendLabel">Opções de salada:</label>
    <GtRadio :options="requestOptions.saladOptions" @optionselected="selectSalad($event, request)" 
      :default="requestOptions.saladOptions[0]" :preselectedoption="request.salad"></GtRadio>
  </div>
</template>

<script>
import GtRadio from './GtRadio'

export default {
  name: 'RequestCard',
  components: {
    GtRadio
  },
  props: {
    request: Object,
    index: Number,
    requestOptions: Object
  },
  methods: {
    selectMeat (value, request) {
			request.meat = value;
		},

		selectSize (value, request) {
			request.size = value;
		},

		selectSalad (value, request) {
			request.salad = value;
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

.cardHead {
  margin-left: 8px;
  margin-right: 8px;
	display: flex; /* Torna o elemento um flex container automaticamente transformando todos os seus filhos diretos em flex itens. */
	flex-direction: row; /* Faz com que os elementos sejam colocados todos em uma coluna, indo de cima para baixo */
	justify-content: space-between;
}

.cardTitle {
	font-size: 24px;
  margin-top: 8px;
  margin-left: 8ox;
}

.cardRemoveButton {
  margin-top: 8px;;
  font-size: 14px;
  width: 40px;
  height: 40px;
}

.legendLabel {
  margin: 0px 0px 0px 32px;
}
</style>