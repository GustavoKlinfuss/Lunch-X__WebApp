<template>
	<div class="requestScreen" :key="keyToReloadScreen">
		<li v-for="(request, index) in requests" v-bind:key="request.id">
			<RequestCard :request="request" :index="index" :requestOptions="requestOptions" @card-excluded="removeCard($event)"></RequestCard>
		</li>
		<b-button size="lg" class="gt-btn" @click="addItem()">Adicionar mais marmita</b-button>
		<b-button size="lg" class="gt-btn" @click="makeRequest()">Fazer pedido</b-button>
	</div>
	
</template>

<script>
import RequestCard from './RequestCard'

var data = {
	requestOptions: {
		meatOptions: ['Frango', 'Bife'],
    sizeOptions: ['Pequena', 'Grande'],
    saladOptions: ['Com tempero', 'Sem tempero'],
	},
	requests: [	],
	keyToReloadScreen: 0
}

export default {
	name: 'RequestsScreen',
	data: function () { return data },
	created: function () {
		if(!this.requests.length) {
			this.addItem()
		}
	},
	components: {
		RequestCard
	},
	methods: {
		makeRequest () {
			console.log('Entrou na função de fazer o pedido')
			var requestList = this.requests
				.map(request => {
					return {
						size: request.size,
						meat: request.meat,
						salad: request.salad
					}
				});

			console.log('Mapeou o pedido para um objeto mais simples')

			const meatOptions = this.requestOptions.meatOptions;
			const sizeOptions = this.requestOptions.sizeOptions;
			const saladOptions = this.requestOptions.saladOptions;
			var message = ""
			var range = [0, 1];

			range.forEach(i => {
				range.forEach(j => {
					const filteredRequest = requestList
						.filter(request => request.meat === meatOptions[i] && request.size === sizeOptions[j])

					if (filteredRequest.length){
						message += filteredRequest.length + ' ' + sizeOptions[j] + ' ' + meatOptions[i] + '\n' 
					}
				})
			})

			message += "\n"

			range.forEach(i => {
				const salad = requestList.filter(request => request.salad === saladOptions[i]);

				if (salad.length) {
					message += salad.length + ' Salada ' + saladOptions[i].toLowerCase() + '\n';
				}
			})

			console.log('Fez a mensagem')
			alert(message)
		},
		addItem: function () {
			const newItem = {
				meat: '',
				size: '',
				salad: ''
			};

			this.requests.push(newItem)
			console.log('Foi adicionado um pedido');
		},
		removeCard: function (index) {
			this.requests.splice(index, 1);
			this.keyToReloadScreen += 1;
			console.log('Foi removido um pedido');
		}
  }
};
</script>

<style scoped>
.requestScreen {
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