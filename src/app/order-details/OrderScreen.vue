<template>
<div class="d-flex flex-column" :key="keyToReloadScreen">
	<li v-for="(item, index) in orderDetails" v-bind:key="item.id">
		<packed-lunch-card 
			v-if="item.itemType === OrderItemTypeEnum.PackedLunch" 
			:item="item" 
			:index="index" 
			v-on:exclude-card="removeCard($event)"/>
		<refrigerant-card 
			v-if="item.itemType === OrderItemTypeEnum.Refrigerant" 
			:item="item" 
			:index="index" 
			v-on:exclude-card="removeCard($event)"/>
	</li>
	<div class="d-flex">
		<base-button 
			class="w-50 mr-1"
			text="Add Packed Lunch" 
			v-on:click="addItemToOrder(OrderItemTypeEnum.PackedLunch)"/>
		<base-button 
			class="w-50 ml-1"
			text="Add Refrigerant"
			v-on:click="addItemToOrder(OrderItemTypeEnum.Refrigerant)"/>
	</div>
	<base-button 
		text="Next Stage" 
		v-on:click="toNextStage()"/>
</div>
</template>

<script>
import PackedLunchCard from './packed-lunch-card/PackedLunchCard.vue'
import RefrigerantCard from './refrigerant-card/RefrigerantCard.vue'
import BaseButton from '../../components/BaseButton.vue'
import { OrderItemTypeEnum } from '../../variables/enums.js'

export default {
	components: {
		PackedLunchCard,
		RefrigerantCard,
		BaseButton
	},
	data: function () { 
		return {
			keyToReloadScreen: 0,
			OrderItemTypeEnum
		}
	},
	props: {
		orderDetails: {type: Array}
	},
	created: function () {
		if(!this.orderDetails.length) {
			this.addItemToOrder(OrderItemTypeEnum.PackedLunch);
		}
	},
	methods: {
		toNextStage: function () {
			this.$emit('step-completed', this.orderDetails);
		},

		addItemToOrder: function (itemType) {
			const newItem = this.getNewItemByItemType(itemType);
			this.orderDetails.push(newItem);
		},

		getNewItemByItemType: function (itemType) {
			if(itemType === OrderItemTypeEnum.PackedLunch) return this.newPackedLunch();
			if(itemType === OrderItemTypeEnum.Refrigerant) return this.newRefrigerant();
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
			this.orderDetails.splice(index, 1);
			this.keyToReloadScreen += 1;
		}
  }
};
</script>

<style scoped>
li {
  list-style-type: none;
}
</style>
