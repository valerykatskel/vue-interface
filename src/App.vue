<template>
	<div id="main-app" class="container">
		<div class="row justify-content-center">
			<add-appointment @add="addItem"/>
			<search-appointments @searchRecords="searchAppointments"/>
			<appointment-list :appointments="filteredApts" @remove="removeItem" @edit="editItem"/>
		</div>
	</div>
</template>

<script>
	import AppointmentList from './components/AppointmentList';
	import AddAppointment from './components/AddAppointment';
	import SearchAppointments from './components/SearchAppointments';
	import _ from 'lodash';
	import axios from 'axios';

	export default {
		name: 'MAinApp',
		data() {
			return {
				title: 'Appointment list',
				appointments: [],
				filterKey: 'petName',
				filterDir: "asc",
				searchTerms: '',
				aptIndex: 0,
			};
		},
		components: {
			AppointmentList,
			AddAppointment,
			SearchAppointments,
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
		computed: {
			searchApts(){
				return this.appointments.filter(apt => 
					apt.petName.toLowerCase().match(this.searchTerms.toLowerCase()) || 
					apt.petOwner.toLowerCase().match(this.searchTerms.toLowerCase()) || 
					apt.aptNotes.toLowerCase().match(this.searchTerms.toLowerCase())
				)
			},
			filteredApts() {
				return _.orderBy(
					this.searchApts,
					item => {
						return item[this.filterKey].toLowerCase();
					}, this.filterDir
				)
			},
		},
		methods: {
			removeItem(apt) {
				this.appointments = _.without(this.appointments, apt);
			},
			editItem(id, field, text) {
				const aptIndex = _.findIndex(this.appointments, {
					aptId: id
				})
				this.appointments[aptIndex][field] = text
			},
			addItem(apt) {
				apt.aptId = this.aptIndex;
				this.aptIndex++
				this.appointments.push(apt);
			},
			searchAppointments(terms){
				this.searchTerms = terms
			},
		},
	};
</script>
