<template>
	<div class="container" :key="keyToReloadScreen">
		<h1 class="header">{{header}}</h1>
			<li v-for="(request, index) in requests" v-bind:key="request.id">
				<RequestCard :request="request" :index="index" :requestOptions="requestOptions" @card-excluded="removeCard($event)"></RequestCard>
			</li>
		<b-button size="lg" class="gt-btn" variant="warning" @click="addItem()">Adicionar mais marmita</b-button>
		<b-button size="lg" class="gt-btn" variant="warning" @click="makeRequest()">Fazer pedido</b-button>
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
	header: 'Tempeadori - Faça seu pedido',
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

<style>
.container {
	font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
	display: flex; /* Torna o elemento um flex container automaticamente transformando todos os seus filhos diretos em flex itens. */
	flex-direction: column; /* Faz com que os elementos sejam colocados todos em uma coluna, indo de cima para baixo */
	font-size: 20px;
}

.header {
	margin-top: 8px;
	padding: 12px;
	background-color: rgb(235, 235, 235);
	border: 1px solid rgb(194, 194, 194);
	border-radius: 8px;
}

li {
  list-style-type: none;
}

.gt-btn {
	margin: 4px 0px 4px 0px;
	border-radius: 20px;
	border: 1px solid green;
}

</style>