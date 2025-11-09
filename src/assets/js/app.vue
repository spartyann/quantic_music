<template>

	<div>
		
		<calculation_table ></calculation_table>
	</div>

</template>

<script>

const { loadModule } = window['vue3-sfc-loader'];

export default {
	
	components: {
		'calculation_table': Vue.defineAsyncComponent( () => loadModule('./assets/js/calculation_table.vue?v=' + VERSION, vueLoaderOptions) ),
	},

	data() {
		let authenticated = localStorage.getItem('authenticated', "1")

		return {
			authenticated : authenticated == "1"
		}
	},


	methods:{
		processAuthenticated()
		{
			localStorage.setItem('authenticated', "1")
			this.authenticated = true;
		},

		logout(){
			localStorage.setItem('authenticated', "0")
			this.authenticated = false;
		}
	}
	
}

</script>
