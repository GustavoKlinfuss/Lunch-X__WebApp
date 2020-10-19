<template>
<base-card titleIcon="basket" cardTitle="Packed Lunch" :index="index" v-on:exclude-card="excludeCard()">
  <span>Meat:</span>
  <base-radio 
    :options="packedLunchOptions.meatOptions" 
    v-model="item.meat"/>

  <span>Size:</span>
  <base-radio 
    :options="packedLunchOptions.sizeOptions" 
    v-model="item.size"/>

  <span>Salad:</span>
  <base-radio 
    :options="packedLunchOptions.saladOptions"
    v-model="item.salad"/>
</base-card>
</template>

<script>
import BaseRadio from '../../../components/BaseRadio.vue'
import BaseCard from '../../../components/BaseCard.vue'
import { RestaurantMenu } from '../../../variables/enums.js'

export default {
  components: {
    BaseRadio,
    BaseCard
  },

  data: function () {
    return {
      packedLunchOptions: {
        meatOptions: this.getMeatOptionsFromThisDay(),
        sizeOptions: ['Large', 'Medium', 'Small'],
        saladOptions: ['With Seasoning', 'Without Seasoning'],
      },
      RestaurantMenu
    }
  },

  props: {
    item: Object,
    index: Number
  },

  methods: {
    getMeatOptionsFromThisDay: function() {
      const thisDayOfWeek = (new Date(Date.now())).getDay();
      const todayMenu = RestaurantMenu[thisDayOfWeek];
      return todayMenu;
    },
    
    excludeCard: function () {
      this.$emit('exclude-card', this.index)
		}
  }
}
</script>
