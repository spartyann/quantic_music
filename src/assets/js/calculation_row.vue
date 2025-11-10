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
			<div><strong>{{ round(audibleFrequence) }} Hz</strong></div>
			<div v-if="show_details">
				Mult par 2: {{ factor2 }}
			</div>
		</td>
		<td>
			<div>{{ notes[noteIndexProche].note }} - {{ notes[noteIndexProche].note2 }}: {{ notes[noteIndexProche].frequence_str }}</div>
			<div>Diff: {{ round(noteDiffFreq) }} Hz</div>
			<div>Diff: {{ round(noteDiffCentT) }} c</div>			
		</td>
		<td>
			<div>{{ deltaEau }} ({{  diapasonEauDemiton }} demis tons + {{ deltaEau - diapasonEauDemiton*100 }})</div>
		</td>
		<td>
			<div>{{ diapasonEauNoteStr }}</div>
		</td>
		<td>
			<a @click="$emit('delete', index)"><i class="fa fa-trash" aria-hidden="true"></i></a>
		</td>
	</tr>

</template>

<style>

	
</style>

<script>

export default {

	props: [ "data", "show_details", "precision", "freq_min_aud", "notes", "index" ],

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
			return this.get2factor(this.frequence, Math.max(10, this.freq_min_aud));
		},

		audibleFrequence(){
			return this.frequence * Math.pow(2, this.factor2);
		},

		noteIndexProche(){
			let frequenceCible = this.audibleFrequence;

			let plusProcheIndex = -1;
			let differenceMin = Infinity;

			for (let i = 0; i < this.notes.length; i++) {
				// Calcule la différence absolue entre la fréquence cible et la fréquence de la note
				const difference = Math.abs(frequenceCible - this.notes[i].frequence);

				// Si cette différence est plus petite que la plus petite différence trouvée jusqu'à présent,
				// cette note devient la nouvelle note la plus proche.
				if (difference < differenceMin) {
					differenceMin = difference;
					plusProcheIndex = i;
				}
			}

			return plusProcheIndex;
		},

		noteDiffFreq(){
			return this.audibleFrequence - this.notes[this.noteIndexProche].frequence;
		},

		noteDiffCentT(){
			return 1200 * Math.log2(this.audibleFrequence / this.notes[this.noteIndexProche].frequence);
		},

		deltaEau(){
			//return this.audibleFrequence * 1.02416
			return Math.round( 1200 * Math.log2(
				(429.62 / (this.frequence * Math.pow(2, this.get2factor(this.frequence, 429.62))))));
		},

		diapasonEauDemiton(){
			//let la = 440;
			let de = this.deltaEau;

			let demiTon = Math.floor(de/100);

			return demiTon;
		},
		diapasonEauIndexNote(){
			let demiTon = this.diapasonEauDemiton;
			let indexNote = demiTon + 49 - 1;

			return indexNote;
		},
		diapasonEauNoteStr(){
			let res =  this.notes[this.diapasonEauIndexNote].note;

			res += " (+ " + (this.deltaEau - (this.diapasonEauDemiton *100)) + ")"

			return res;
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

		get2factor(frequence, freqMin){

			
			let freqMax = freqMin * 2;

			// Gérer les cas de fréquences non valides
			if (frequence <= 0) {
				console.error("La fréquence doit être un nombre positif.");
				return null;
			}

			// Si la fréquence est déjà dans la plage souhaitée, aucun changement n'est nécessaire
			if (frequence >= freqMin && frequence <= freqMax) {
				return 0;
			}

			let freqActuelle = frequence;
  			let x = 0;

			// Si la fréquence est trop élevée, on la divise par 2 jusqu'à ce qu'elle soit dans la plage.
			// On décrémente x à chaque division.
			while (freqActuelle > freqMax) {
				freqActuelle /= 2;
				x--;
			}

			// Si la fréquence est trop basse, on la multiplie par 2 jusqu'à ce qu'elle soit dans la plage.
			// On incrémente x à chaque multiplication.
			while (freqActuelle < freqMin) {
				freqActuelle *= 2;
				x++;
			}

			return x;
		}

	}
}

</script>

