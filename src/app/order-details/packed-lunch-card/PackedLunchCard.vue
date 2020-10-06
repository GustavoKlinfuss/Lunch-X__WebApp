<template>
<div class="card">
  <div class="card-head">
    <label class="card-title">
      <b-icon icon="basket"></b-icon>
      Item {{index + 1}} - Marmita
    </label>
    <b-button class="card-remove-button" variant="danger" v-on:click="excludeCard(index)">X</b-button>
  </div>
  
  <label class="legend-label">Carne:</label>
  <GtRadio :options="packedLunchOptions.meatOptions" v-on:optionselected="selectMeat($event, order)"
    :default="packedLunchOptions.meatOptions[0]" :preselectedoption="order.meat"></GtRadio>

  <label class="legend-label">Tamanho:</label>
  <GtRadio :options="packedLunchOptions.sizeOptions" v-on:optionselected="selectSize($event, order)" 
    :default="packedLunchOptions.sizeOptions[0]" :preselectedoption="order.size"></GtRadio>

  <label class="legend-label">Salada:</label>
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
  data: function () {
    return {
      packedLunchOptions: {
        meatOptions: ['Frango', 'Bife'],
        sizeOptions: ['Pequena', 'Grande'],
        saladOptions: ['Com tempero', 'Sem tempero'],
      }
    }
  },
  props: {
    order: Object,
    index: Number
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