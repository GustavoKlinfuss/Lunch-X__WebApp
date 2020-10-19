<template>
<base-card titleIcon="basket" cardTitle="Packed Lunch" :index="index" v-on:exclude-card="excludeCard()">
  <span>Meat:</span>
  <gt-radio 
    :options="packedLunchOptions.meatOptions" 
    v-model="item.meat"/>

  <span>Size:</span>
  <gt-radio 
    :options="packedLunchOptions.sizeOptions" 
    v-model="item.size"/>

  <span>Salad:</span>
  <gt-radio 
    :options="packedLunchOptions.saladOptions"
    v-model="item.salad"/>
</base-card>
</template>

<script>
import GtRadio from '../../../components/GtRadio.vue'
import BaseCard from '../../../components/BaseCard.vue'
import { RestaurantMenu } from '../../../variables/enums.js'

export default {
  components: {
    GtRadio,
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
