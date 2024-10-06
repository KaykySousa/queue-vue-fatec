<script setup lang="ts">
import { ref } from "vue"

const queue = ref<string[]>([])
const specialQueue = ref<string[]>([])

const currentTicket = ref(0)
const currentSpecialTicket = ref(0)

const attendedTicket = ref<string>()

function generateTicket() {
	queue.value.push(`C${(++currentTicket.value).toString().padStart(4, "0")}`)
}

function generateSpecialTicket() {
	specialQueue.value.push(`P${(++currentSpecialTicket.value).toString().padStart(4, "0")}`)
}

function attendTicket() {
	attendedTicket.value = queue.value.shift()
}

function attendSpecialTicket() {
	attendedTicket.value = specialQueue.value.shift()
}
</script>

<template>
	<main>
		<section>
			<h1>Gerar Senha</h1>
			<button v-on:click="generateTicket">Gerar Senha</button>
			<button v-on:click="generateSpecialTicket">Gerar Senha Especial</button>
		</section>
		<section class="queue-container">
			<div v-if="queue.length">
				<h1>Fila Comum</h1>
				<ul>
					<li v-for="ticket in queue" :key="ticket">
						{{ ticket }}
					</li>
				</ul>
			</div>

			<div v-if="specialQueue.length">
				<h1>Fila Especial</h1>
				<ul>
					<li v-for="ticket in specialQueue" :key="ticket">
						{{ ticket }}
					</li>
				</ul>
			</div>
		</section>
		<section>
			<h1>Atendimento</h1>
			<button v-on:click="attendTicket">Atender</button>
			<button v-on:click="attendSpecialTicket">Atender Especial</button>
		</section>
		<section>
			<p v-if="attendedTicket">Senha Atendida: {{ attendedTicket }}</p>
			<p v-else>Aguarde ser chamado</p>
		</section>
	</main>
</template>
