<template>

	<div class="container">
		<div class="row">
			<div class="col-12">

				<h1>Notes</h1>

				<table class="table table-bordered table-sm ">
					<thead>
						<tr>
							<th>Note</th>
							<th>Note</th>
							<th>Octave</th>
							<th>Fréquence</th>
						</tr>
					</thead>
					<tbody>
						<tr v-for="(note) in notes">
							<td>{{ note.note }}</td>
							<td>{{ note.note2 }}</td>
							<td>{{ note.octave }}</td>
							<td>{{ note.frequence_str }}</td>
						</tr>
					</tbody>
				</table>
			</div>
		</div>
	</div>

</template>

<style>

	
</style>

<script>

const { loadModule } = window['vue3-sfc-loader'];

export default {
	
	props: ["notes"],

	data() {

		return {
			 
		}
	},

	watch: {
		
	},

	mounted() {
		
	},

	computed: {
		

	},

	methods: {

		

	}
}

</script>

