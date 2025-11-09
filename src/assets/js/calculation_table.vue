<template>

	<div class="container">
		<div class="row">
			<div class="col-12">

				<h1>Calculs</h1>

				<div class="my-3">
					<p>Décimales: <input type="number" step="1" min="0" max="10" v-model="precision" class="form-control d-inline me-2" style="max-width: 70px;"/></p>

					<p>Freq Min audible: <input type="number" min="1" max="100000" step="100" v-model="freq_min_aud" class="form-control d-inline me-2" style="max-width: 100px;"/></p>

					<div class="form-check">
						<input class="form-check-input" type="checkbox" value="" id="checkShowDetails" v-model="show_details">
						<label class="form-check-label" for="checkShowDetails">
							Afficher les détails
						</label>
					</div>
				</div>

				<table class="table table-bordered table-sm ">
					<thead>
						<tr>
							<th>Nom</th>
							<th>Masse</th>
							<th>Fréquence</th>
							<th>Note proche</th>
							<th>Delta au Diapason Eau</th>
							<th>Note au Diapason Eau</th>
							<th></th>
						</tr>
					</thead>
					<tbody>
						<calculation_row v-for="(row, index) in rows"
							:data="row"
							:index="index"
							:show_details="show_details"
							:precision="precision"
							:freq_min_aud="freq_min_aud"
							:notes="notes"
							@delete="deleteRow"
							></calculation_row>
					</tbody>
				</table>

				<p>
					<button class="btn btn-primary" @click="addRow">
						Ajouter une ligne
					</button>
					&nbsp;

					<button class="btn btn-primary" @click="save">
						Enregistrer
					</button>
				</p>
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

	props: ["notes"],

	data() {

		let rows = JSON.parse(localStorage.getItem('rows1', "null"));

		if (rows == null) rows =  [ 
			{ name: "Soleil", masse: 1.99890, masse_p: 30, masse_unite: "kg", },
			{ name: "Mercure", masse: 3.30180, masse_p: 23, masse_unite: "kg", },
			{ name: "Vénus", masse: 4.86850, masse_p: 24, masse_unite: "kg", },
			{ name: "Lune", masse: 7.34200, masse_p: 22, masse_unite: "kg", },
			{ name: "Terre", masse: 5.97360, masse_p: 24, masse_unite: "kg", },
		];

		return {
			precision: 2,
			freq_min_aud: 400,
			show_details: false,
			rows: rows
		}
	},

	watch: {
		
	},

	mounted() {
		
	},

	computed: {
		

	},

	methods: {
		save(){
			localStorage.setItem('rows1', JSON.stringify(this.rows))
			alert("Enregistré !")
		},
		addRow(){
			this.rows.push({ name: "Terre", masse: 5.97360, masse_p: 24, masse_unite: "kg", });
		},

		deleteRow(index){
			this.rows.splice(index, 1);
		}

	}
}

</script>
