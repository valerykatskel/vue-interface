<template>
	<div id="main-app" class="container">
		<div class="row justify-content-center">
			<appointment-list :appointments="appointments" />
		</div>
	</div>
</template>

<script>
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
			AppointmentList,
		},
		mounted() {
			axios
				.get('./data/appointments.json')
				.then(resp => (this.appointments = resp.data));
		},
	};
</script>
