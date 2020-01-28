<template>
	<div id="main-app" class="container">
		<h4>{{ title }}</h4>
		<font-awesome-icon icon="plus" class="mr-2" /> Add appointment
		<appointment-list :appointments="appointments" />
	</div>
</template>

<script>
	import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome';
	import AppointmentList from './components/AppointmentList';
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
			AppointmentList,
		},
		mounted() {
			axios
				.get('./data/appointments.json')
				.then(resp => (this.appointments = resp.data));
		},
	};
</script>
