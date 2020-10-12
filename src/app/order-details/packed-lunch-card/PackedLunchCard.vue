<template>
<gt-card headerIcon="basket" :index="index" headerText="Marmita" v-on:exclude-card="excludeCard()">
  <gt-label text="Carne:"/>
  <gt-radio :options="packedLunchOptions.meatOptions" v-model="item.meat"/>

  <gt-label text="Tamanho:"/>
  <gt-radio :options="packedLunchOptions.sizeOptions" v-model="item.size"/>

  <gt-label text="Salada:"/>
  <gt-radio :options="packedLunchOptions.saladOptions" v-model="item.salad"/>
</gt-card>
</template>

<script>
import GtRadio from '../../../components/GtRadio.vue'
import GtLabel from '../../../components/GtLabel.vue'
import { RestaurantMenu } from '../../../variables/enums.js'
import GtCard from '../../../components/GtCard.vue'

export default {
  name: 'RequestCard',
  components: {
    GtRadio,
    GtLabel,
    GtCard
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
