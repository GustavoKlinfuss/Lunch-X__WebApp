<template>
<div class="card">
  <div class="card-head">
    <label class="card-title">
      <b-icon icon="basket"></b-icon>
      Item {{index + 1}} - Marmita
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
      Remover marmita
    </b-button>
  </div>
  
  <label class="legend-label">Carne:</label>
  <gt-radio 
    :options="packedLunchOptions.meatOptions" 
    v-on:optionselected="selectMeat($event, order)"
    :default="packedLunchOptions.meatOptions[0]" 
    :preselectedoption="order.meat"/>

  <label class="legend-label">Tamanho:</label>
  <gt-radio 
    :options="packedLunchOptions.sizeOptions" 
    v-on:optionselected="selectSize($event, order)" 
    :default="packedLunchOptions.sizeOptions[0]" 
    :preselectedoption="order.size"/>

  <label class="legend-label">Salada:</label>
  <gt-radio 
    :options="packedLunchOptions.saladOptions" 
    v-on:optionselected="selectSalad($event, order)" 
    :default="packedLunchOptions.saladOptions[0]" 
    :preselectedoption="order.salad"/>
</div>
</template>

<script>
import GtRadio from '../../../components/GtRadio.vue'
import { RestaurantMenu } from '../../../variables/enums.js'

export default {
  name: 'RequestCard',
  components: {
    GtRadio
  },
  data: function () {
    return {
      packedLunchOptions: {
        meatOptions: this.getMeatOptionsFromThisDay(),
        sizeOptions: ['Grande', 'Pequena'],
        saladOptions: ['Com tempero', 'Sem tempero'],
      },
      RestaurantMenu
    }
  },
  props: {
    order: Object,
    index: Number
  },
  methods: {
    getMeatOptionsFromThisDay: function() {
      const todayInDayOfWeek = (new Date(Date.now())).getDay();
      const todayMenu = RestaurantMenu[todayInDayOfWeek];
      return todayMenu;
    },
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
