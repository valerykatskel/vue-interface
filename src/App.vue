<template>
	<div id="main-app" class="container">
		<h4>{{ title }}</h4>
		<font-awesome-icon icon="plus" class="mr-2" /> Add appointment
		<div v-for="(item, i) in appointments" :key="i">
			<h4>{{ item.petName }}</h4>
			<p>{{ item.aptNotes }}</p>
		</div>
	</div>
</template>

<script>
	import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome';
	import axios from 'axios';

	export default {
		name: 'MAinApp',
		data() {
			return {
				title: 'Appointment list',
				appointments: [],
			};
		},
		components: {
			FontAwesomeIcon,
		},
		mounted() {
			axios
				.get('./data/appointments.json')
				.then(resp => (this.appointments = resp.data));
		},
	};
</script>
