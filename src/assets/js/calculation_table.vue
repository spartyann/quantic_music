<template>

	<div class="container">
		<div class="row">
			<div class="col-12">

				<h1>Calculs</h1>

				<div class="my-3">
					Précision: <input type="number" step="1" min="0" max="10" v-model="precision" class="form-control d-inline me-2" style="max-width: 70px;"/>

					Freq Min audible: <input type="number" min="1" max="100000" step="100" v-model="freq_min_aud" class="form-control d-inline me-2" style="max-width: 100px;"/>

				</div>

				<table class="table table-bordered table-sm ">
					<thead>
						<tr>
							<th>Nom</th>
							<th>Masse</th>
							<th>Fréquence</th>
							<th></th>
						</tr>
					</thead>
					<tbody>
						<calculation_row v-for="(row) in rows"
							:data="row"
							:show_details="true"
							:precision="precision"
							:freq_min_aud="freq_min_aud"
							></calculation_row>
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
	
	components: {
		'calculation_row': Vue.defineAsyncComponent( () => loadModule('./assets/js/calculation_row.vue?v=' + VERSION, vueLoaderOptions) ),
	},

	data() {
		return {
			precision: 2,
			freq_min_aud: 1000,
			rows: [ 
				{ name: "Soleil", masse: 1.99890, masse_p: 30, masse_unite: "kg", },
				{ name: "Mercure", masse: 3.30180, masse_p: 23, masse_unite: "kg", },
				{ name: "Vénus", masse: 4.86850, masse_p: 24, masse_unite: "kg", },
				{ name: "Lune", masse: 7.34200, masse_p: 22, masse_unite: "kg", },
				{ name: "Terre", masse: 5.97360, masse_p: 24, masse_unite: "kg", },
		]
			
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
