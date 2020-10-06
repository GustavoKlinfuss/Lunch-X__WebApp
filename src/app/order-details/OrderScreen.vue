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
			text="+ Marmita" 
			v-on:click="addItemToOrder(OrderItemTypeEnum.PackedLunch)"/>
		<GtButton 
			style="margin-left: 1%; width: 49.5%" 
			text="+ Refrigerante" 
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

var data = {
	
}

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

			// console.log('Entrou na função de fazer o pedido')
			// var orderList = this.orders
			// 	.map(order => {
			// 		return {
			// 			size: order.size,
			// 			meat: order.meat,
			// 			salad: order.salad
			// 		}
			// 	});

			// console.log('Mapeou o pedido para um objeto mais simples')

			// const meatOptions = this.packedLunchOptions.meatOptions;
			// const sizeOptions = this.packedLunchOptions.sizeOptions;
			// const saladOptions = this.packedLunchOptions.saladOptions;
			// var message = ""
			// var range = [0, 1];

			// range.forEach(i => {
			// 	range.forEach(j => {
			// 		const filteredRequest = orderList
			// 			.filter(order => order.meat === meatOptions[i] && order.size === sizeOptions[j])

			// 		if (filteredRequest.length){
			// 			message += filteredRequest.length + ' ' + sizeOptions[j] + ' ' + meatOptions[i] + '\n' 
			// 		}
			// 	})
			// })

			// message += "\n"

			// range.forEach(i => {
			// 	const salad = orderList.filter(order => order.salad === saladOptions[i]);

			// 	if (salad.length) {
			// 		message += salad.length + ' Salada ' + saladOptions[i].toLowerCase() + '\n';
			// 	}
			// })

			// console.log('Fez a mensagem')
			// alert(message)
		},
		addItemToOrder: function (itemType) {
			let newItem = {};

			if(itemType === OrderItemTypeEnum.PackedLunch) {
				newItem = this.newPackedLunch();
			}
			else if(itemType === OrderItemTypeEnum.Refrigerant) {
				newItem = this.newRefrigerant();
			} else {
				throw "Não foi selecionado nem marmita, nem refrigerante";
			}

			this.orders.push(newItem)
			console.log('Foi adicionado um pedido');
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
			console.log('Foi removido um pedido');
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