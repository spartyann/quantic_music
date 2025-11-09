<template>

	<div class="container">
		<div class="row">
			<div class="col-12">

				<h1>Calculs</h1>


				<table class="table table-bordered table-sm ">
					<thead>
						<tr>
							<th>Nom</th>
							<th>Masse</th>
							<th>Fréquence</th>
						</tr>
					</thead>
					<tbody>
						<calculation_row v-for="(row) in rows" :data="row"></calculation_row>
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
