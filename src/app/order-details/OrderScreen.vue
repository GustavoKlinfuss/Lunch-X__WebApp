<template>
<div class="order-screen" :key="keyToReloadScreen">
	<li v-for="(order, index) in orders" v-bind:key="order.id">
		<PackedLunchCard 
			v-if="order.itemType === OrderItemTypeEnum.PackedLunch" 
			:order="order" 
			:index="index" 
			v-on:card-excluded="removeCard($event)"/>
		<RefrigerantCard 
			v-if="order.itemType === OrderItemTypeEnum.Refrigerant" 
			:order="order" 
			:index="index" 
			v-on:card-excluded="removeCard($event)"/>
	</li>
	<div class="row-div">
		<GtButton 
			style="width: 49.5%" 
			text="Adicionar Marmita" 
			v-on:click="addItemToOrder(OrderItemTypeEnum.PackedLunch)"/>
		<GtButton 
			style="margin-left: 1%; width: 49.5%" 
			text="Adicionar Refrigerante"
			v-on:click="addItemToOrder(OrderItemTypeEnum.Refrigerant)"/>
	</div>
	<GtButton 
		text="Próxima etapa"
		v-on:click="finishOrder()"/>
</div>
</template>

<script>
import PackedLunchCard from './packed-lunch-card/PackedLunchCard.vue'
import RefrigerantCard from './refrigerant-card/RefrigerantCard.vue'
import GtButton from '../../components/GtButton.vue'

const OrderItemTypeEnum = Object.freeze({
	"PackedLunch":1,
	"Refrigerant":2
});

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
.order-screen {
	display: flex;
	flex-direction: column;
}

.gt-btn {
	margin: 4px 0px 4px 0px;
	border-radius: 0px;
	background-color:  rgb(0, 50, 107);
	border: 1px solid white;
}
</style>