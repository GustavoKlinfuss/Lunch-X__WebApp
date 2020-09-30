<template>
	<div class="container" :key="keyToReload">
		<h1 class="header">{{header}}</h1>
			<li v-for="(request, index) in requests" v-bind:key="request.id">
				<GtItemCard :request="request" :index="index" :generalOptions="generalOptions" @card-excluded="removeCard($event)"></GtItemCard>
			</li>
		<b-button size="lg" class="gt-btn" variant="warning" @click="addRequest()">Adicionar mais marmita</b-button>
		<b-button size="lg" class="gt-btn" variant="warning" @click="makeRequest()">Fazer pedido</b-button>
	</div>
	
</template>

<script>

import GtItemCard from './GtItemCard'

var data = {
	generalOptions: {
		meatOptions: ['Frango', 'Bife'],
    sizeOptions: ['Pequena', 'Grande'],
    saladOptions: ['Com tempero', 'Sem tempero'],
	},
	requests: [
			{
					meat: '',
					size: '',
					salad: ''
			}
	],
	header: 'Tempeadori - Faça seu pedido',
	keyToReload: 0
}

export default {
	name: 'Main',
	data: function () {
			return data
	},
	components: {
		GtItemCard
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

			const meatOptions = this.generalOptions.meatOptions;
			const sizeOptions = this.generalOptions.sizeOptions;
			const saladOptions = this.generalOptions.saladOptions;
			var requestMessage = ""
			var range = [0, 1];

			range.forEach(i => {
				range.forEach(j => {
					var filteredRequest = requestList
						.filter(request => request.meat === meatOptions[i] && request.size === sizeOptions[j])

					if (filteredRequest.length){
						requestMessage += filteredRequest.length + ' ' + sizeOptions[j] + ' ' + meatOptions[i] + '\n' 
					}
				})
			})

			requestMessage += "\n"

			range.forEach(i => {
				var salad = requestList.filter(request => request.salad === saladOptions[i]);
				if (salad.length) requestMessage += salad.length + ' Salada ' + saladOptions[i].toLowerCase() + '\n';
			})

			console.log('Fez a mensagem')

			alert(requestMessage)
		},
		addRequest: function () {
			this.requests.push({
				meat: '',
				size: '',
				salad: ''
			})
		},
		removeCard: function (index) {
			this.requests.splice(index, 1);
			this.keyToReload += 1;
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
	padding: 8px;
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