<template>
	<div id="main-app" class="container">
		<div class="row justify-content-center">
			<appointment-list :appointments="appointments" @remove="removeItem" @edit="editItem"/>
		</div>
	</div>
</template>

<script>
	import AppointmentList from './components/AppointmentList';
	import _ from 'lodash';
	import axios from 'axios';

	export default {
		name: 'MAinApp',
		data() {
			return {
				title: 'Appointment list',
				appointments: [],
				aptIndex: 0,
			};
		},
		components: {
			AppointmentList,
		},
		mounted() {
			axios.get('./data/appointments.json').then(
				resp =>
					(this.appointments = resp.data.map(item => {
						item.aptId = this.aptIndex++;
						return item;
					}))
			);
		},
		methods: {
			removeItem(apt) {
				this.appointments = _.without(this.appointments, apt);
			},
			editItem: function(id, field, text) {
				const aptIndex = _.findIndex(this.appointments, {
					aptId: id
				})
				this.appointments[aptIndex][field] = text
			}
		},
	};
</script>
