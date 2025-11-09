<template>

	<tr>
		<td>
			<input v-model="data.name" class="form-control d-inline me-2" style="max-width: 150px;"/>
		</td>
		<td class="white-space-nowrap" >
			<div>
				<input type="number" step="0.0001" v-model="data.masse" class="form-control d-inline me-2" style="max-width: 150px;"/>
				x10^
				<input type="number" step="1" v-model="data.masse_p" class="form-control d-inline me-2" style="max-width: 70px;"/>
				<select class="form-control d-inline" v-model="data.masse_unite" style="max-width: 50px;">
					<option value="kg" name="kg">Kg</option>
					<option value="da" name="da">Da</option>
				</select>
			</div>
			<div v-if="data.masse_unite == 'da'">
				= {{ masse }} Kg
			</div>
		</td>
		<td>
			{{ round(audibleFrequence) }} Hz
		</td>
		<td>

		</td>
	</tr>

</template>

<style>

	
</style>

<script>

export default {

	props: [ "data", "show_details", "precision", "freq_min_aud" ],

	data() {
		return {


			
		}
	},

	watch: {
		
	},

	mounted() {
		
	},

	computed: {
		masse(){
			let masse = (this.data.masse * Math.pow(10, this.data.masse_p));
			if (this.data.masse_unite == "da") masse = masse / (6.02214 * Math.pow(10,26));
			return masse;
		},

		frequence(){
			return this.masse2freq(this.masse);
		},

		factor2(){
			return this.get2factor(this.frequence);
		},

		audibleFrequence(){
			return this.frequence * Math.pow(2, this.factor2);
		}
	},

	methods: {

		round(val) {

			let prec = Math.pow(10, Math.max(0, this.precision));
			return Math.round(val * prec) / prec
		},
		masse2freq(masse){
			return masse * (Math.pow(299792458,2) / (6.62607015 * Math.pow(10,-34)));
		},

		get2factor(frequence){

			let FREQ_MIN = Math.max(10, this.freq_min_aud);
			let FREQ_MAX = FREQ_MIN * 2;

			// Gérer les cas de fréquences non valides
			if (frequence <= 0) {
				console.error("La fréquence doit être un nombre positif.");
				return null;
			}

			// Si la fréquence est déjà dans la plage souhaitée, aucun changement n'est nécessaire
			if (frequence >= FREQ_MIN && frequence <= FREQ_MAX) {
				return 0;
			}

			let freqActuelle = frequence;
  			let x = 0;

			// Si la fréquence est trop élevée, on la divise par 2 jusqu'à ce qu'elle soit dans la plage.
			// On décrémente x à chaque division.
			while (freqActuelle > FREQ_MAX) {
				freqActuelle /= 2;
				x--;
			}

			// Si la fréquence est trop basse, on la multiplie par 2 jusqu'à ce qu'elle soit dans la plage.
			// On incrémente x à chaque multiplication.
			while (freqActuelle < FREQ_MIN) {
				freqActuelle *= 2;
				x++;
			}

			return x;
		}

	}
}

</script>

