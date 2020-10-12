<template>
<div class="d-flex flex-column" :key="keyToReloadScreen">
	<li v-for="(item, index) in order" v-bind:key="item.id">
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
		<gt-button 
			class="w-50 mr-1"
			text="Adicionar Marmita" 
			v-on:click="addItemToOrder(OrderItemTypeEnum.PackedLunch)"/>
		<gt-button 
			class="w-50 ml-1"
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
	components: {
		PackedLunchCard,
		RefrigerantCard,
		GtButton
	},
	data: function () { 
		return {
			order: [	],
			keyToReloadScreen: 0,
			OrderItemTypeEnum
		}
	},
	created: function () {
		if(!this.order.length) {
			this.addItemToOrder(OrderItemTypeEnum.PackedLunch);
		}
	},
	methods: {
		finishOrder: function () {
			this.$emit('step-completed', this.order);
		},

		addItemToOrder: function (itemType) {
			const newItem = this.getNewItemByItemType(itemType);
			this.order.push(newItem);
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
			this.order.splice(index, 1);
			this.keyToReloadScreen += 1;
		}
  }
};
</script>
