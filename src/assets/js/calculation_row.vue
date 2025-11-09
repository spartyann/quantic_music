<template>

	<tr>
		<td>
			<input v-model="data.name" class="form-control d-inline me-2" style="max-width: 150px;"/>
		</td>
		<td class="white-space-nowrap" >
			<input type="number" step="0.0001" v-model="data.masse" class="form-control d-inline me-2" style="max-width: 150px;"/>
			x10^
			<input type="number" step="1" v-model="data.masse_p" class="form-control d-inline me-2" style="max-width: 70px;"/>
			<select class="form-control d-inline" v-model="data.masse_unite" style="max-width: 50px;">
				<option value="kg" name="kg">Kg</option>
				<option value="da" name="da">Da</option>
			</select>
		</td>
		<td>
			
		</td>
		<td><pre>{{ data }}</pre></td>
	</tr>

</template>

<style>

	
</style>

<script>

export default {

	props: [ "data" ],

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

