<template>
<div class="order-screen" :key="keyToReloadScreen">
	<li v-for="(order, index) in orders" v-bind:key="order.id">
		<PackedLunchCard :order="order" :index="index" :packedLunchOptions="packedLunchOptions" v-on:card-excluded="removeCard($event)"/>
	</li>
	<GtButton text="Adicionar mais marmita" v-on:click="addItemToOrder()"/>
	<GtButton text="Próxima etapa" v-on:click="finishOrder()"/>
</div>
</template>

<script>
import PackedLunchCard from './packed-lunch-card/PackedLunchCard.vue'
import GtButton from '../../components/GtButton.vue'

var data = {
	packedLunchOptions: {
		meatOptions: ['Frango', 'Bife'],
    sizeOptions: ['Pequena', 'Grande'],
    saladOptions: ['Com tempero', 'Sem tempero'],
	},
	orders: [	],
	keyToReloadScreen: 0
}

export default {
	name: 'OrderScreen',
	data: function () { return data },
	created: function () {
		if(!this.orders.length) {
			this.addItemToOrder()
		}
	},
	components: {
		PackedLunchCard,
		GtButton
	},
	methods: {
		finishOrder () {
			this.$emit('step-completed', this.orders)

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
		addItemToOrder: function () {
			const newItem = {
				meat: '',
				size: '',
				salad: ''
			};

			this.orders.push(newItem)
			console.log('Foi adicionado um pedido');
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