<template>
<div class="column-div" :key="keyToReloadScreen">
	<li v-for="(order, index) in orders" v-bind:key="order.id">
		<packed-lunch-card 
			class="order-card"
			v-if="order.itemType === OrderItemTypeEnum.PackedLunch" 
			:order="order" 
			:index="index" 
			v-on:card-excluded="removeCard($event)"/>
		<refrigerant-card 
			class="order-card"
			v-if="order.itemType === OrderItemTypeEnum.Refrigerant" 
			:order="order" 
			:index="index" 
			v-on:card-excluded="removeCard($event)"/>
	</li>
	<div class="row-div">
		<gt-button 
			style="width: 49%" 
			text="Adicionar Marmita" 
			v-on:click="addItemToOrder(OrderItemTypeEnum.PackedLunch)"/>
		<gt-button 
			style="margin-left: 2%; width: 49%" 
			text="Adicionar Refrigerante"
			v-on:click="addItemToOrder(OrderItemTypeEnum.Refrigerant)"/>
	</div>
	<gt-button 
		text="Próxima etapa"
		v-on:click="finishOrder()"/>
</div>
</template>

<script>
import PackedLunchCard from './packed-lunch-card/PackedLunchCard.vue'
import RefrigerantCard from './refrigerant-card/RefrigerantCard.vue'
import GtButton from '../../components/GtButton.vue'
import { OrderItemTypeEnum } from '../../variables/enums.js'

export default {
	name: 'OrderScreen',
	components: {
		PackedLunchCard,
		RefrigerantCard,
		GtButton
	},
	data: function () { 
		return {
			orders: [	],
			keyToReloadScreen: 0,
			OrderItemTypeEnum
		}
	},
	created: function () {
		if(!this.orders.length) {
			this.addItemToOrder(OrderItemTypeEnum.PackedLunch);
		}
	},
	methods: {
		finishOrder: function () {
			this.$emit('step-completed', this.orders);
		},

		addItemToOrder: function (itemType) {
			const newItem = this.getNewItemByItemType(itemType);
			this.orders.push(newItem);
		},

		getNewItemByItemType: function (itemType) {
			if(itemType === OrderItemTypeEnum.PackedLunch) return this.newPackedLunch();
			if(itemType === OrderItemTypeEnum.Refrigerant) return this.newRefrigerant();
			
			throw "Não foi selecionado nem marmita, nem refrigerante";
		},
		
		newPackedLunch: function() {
			return {
				itemType: OrderItemTypeEnum.PackedLunch,
				meat: '',
				size: '',
				salad: ''
			};
		},

		newRefrigerant: function() {
			return {
				itemType: OrderItemTypeEnum.Refrigerant,
				refrigerantSize: '',
				refrigerantType: ''
			};
		},
		
		removeCard: function (index) {
			this.orders.splice(index, 1);
			this.keyToReloadScreen += 1;
		}
  }
};
</script>

<style scoped>
.order-card {
  background-color: rgb(235, 235, 235);
  padding-bottom: 8px;
  margin-bottom: 8px;
}

.order-card >>> .card-head {
  margin-left: 8px;
  margin-right: 8px;
	display: flex;
	flex-direction: row;
	justify-content: space-between;
}

.order-card >>> .card-title {
	font-size: 20px;
  margin-top: 8px;
  margin-left: 8px;
  font-weight: bolder;
}

.order-card >>> .card-remove-button {
  margin-top: 8px;
  font-size: 14px;
}

.order-card >>> .legend-label {
  margin: 0px 0px 0px 32px;
}
</style>
