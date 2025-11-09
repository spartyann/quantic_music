<template>

	<div>
		
		<calculation_table :notes="notes"></calculation_table>
		<notes :notes="notes"></notes>
	</div>

</template>

<script>

const { loadModule } = window['vue3-sfc-loader'];

export default {
	
	components: {
		'calculation_table': Vue.defineAsyncComponent( () => loadModule('./assets/js/calculation_table.vue?v=' + VERSION, vueLoaderOptions) ),
		'notes': Vue.defineAsyncComponent( () => loadModule('./assets/js/notes.vue?v=' + VERSION, vueLoaderOptions) ),
	},

	data() {
		let authenticated = localStorage.getItem('authenticated', "1")

		return {
			authenticated : authenticated == "1",
			notes: this.genererToutesLesNotes()
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
		},



		genererToutesLesNotes() {
			const nomsDeNotes = ['A', 'A#', 'B', 'C', 'C#', 'D', 'D#', 'E', 'F', 'F#', 'G', 'G#'];
			const noms2DeNotes = ['La', 'La#', 'Si', 'Do', 'Do#', 'Ré', 'Ré#', 'Mi', 'Fa', 'Fa#', 'Sol', 'Sol#'];
			const frequenceA4 = 440; // Fréquence de référence pour le La 4
			const toutesLesNotes = [];

			let notes = [
				{ note: 'A0', frequence: 27.5 },
				{ note: 'A#0', frequence: 29.14 },
				{ note: 'B0', frequence: 30.87 },
				{ note: 'C1', frequence: 32.7 },
				{ note: 'C#1', frequence: 34.65 },
				{ note: 'D1', frequence: 36.71 },
				{ note: 'D#1', frequence: 38.89 },
				{ note: 'E1', frequence: 41.2 },
				{ note: 'F1', frequence: 43.65 },
				{ note: 'F#1', frequence: 46.25 },
				{ note: 'G1', frequence: 49 },
				{ note: 'G#1', frequence: 51.96 },
				{ note: 'A1', frequence: 55 },
				{ note: 'A#1', frequence: 58.27 },
				{ note: 'B1', frequence: 61.74 },
				{ note: 'C2', frequence: 65.41 },
				{ note: 'C#2', frequence: 69.3 },
				{ note: 'D2', frequence: 73.42 },
				{ note: 'D#2', frequence: 77.78 },
				{ note: 'E2', frequence: 82.41 },
				{ note: 'F2', frequence: 87.31 },
				{ note: 'F#2', frequence: 92.5 },
				{ note: 'G2', frequence: 98 },
				{ note: 'G#2', frequence: 103.83 },
				{ note: 'A2', frequence: 110 },
				{ note: 'A#2', frequence: 116.54 },
				{ note: 'B2', frequence: 123.47 },
				{ note: 'C3', frequence: 130.81 },
				{ note: 'C#3', frequence: 138.59 },
				{ note: 'D3', frequence: 146.83 },
				{ note: 'D#3', frequence: 155.56 },
				{ note: 'E3', frequence: 164.81 },
				{ note: 'F3', frequence: 174.61 },
				{ note: 'F#3', frequence: 185 },
				{ note: 'G3', frequence: 196 },
				{ note: 'G#3', frequence: 207.65 },
				{ note: 'A3', frequence: 220 },
				{ note: 'A#3', frequence: 233.08 },
				{ note: 'B3', frequence: 246.94 },
				{ note: 'C4', frequence: 261.63 },
				{ note: 'C#4', frequence: 277.18 },
				{ note: 'D4', frequence: 293.66 },
				{ note: 'D#4', frequence: 311.13 },
				{ note: 'E4', frequence: 329.63 },
				{ note: 'F4', frequence: 349.23 },
				{ note: 'F#4', frequence: 369.99 },
				{ note: 'G4', frequence: 392 },
				{ note: 'G#4', frequence: 415.3 },
				{ note: 'A4', frequence: 440 },
				{ note: 'A#4', frequence: 466.16 },
				{ note: 'B4', frequence: 493.88 },
				{ note: 'C5', frequence: 523.25 },
				{ note: 'C#5', frequence: 554.37 },
				{ note: 'D5', frequence: 587.33 },
				{ note: 'D#5', frequence: 622.25 },
				{ note: 'E5', frequence: 659.25 },
				{ note: 'F5', frequence: 698.46 },
				{ note: 'F#5', frequence: 739.99 },
				{ note: 'G5', frequence: 783.99 },
				{ note: 'G#5', frequence: 830.61 },
				{ note: 'A5', frequence: 880 },
				{ note: 'A#5', frequence: 932.33 },
				{ note: 'B5', frequence: 987.77 },
				{ note: 'C6', frequence: 1046.5 },
				{ note: 'C#6', frequence: 1108.73 },
				{ note: 'D6', frequence: 1174.66 },
				{ note: 'D#6', frequence: 1244.51 },
				{ note: 'E6', frequence: 1318.51 },
				{ note: 'F6', frequence: 1396.91 },
				{ note: 'F#6', frequence: 1479.98 },
				{ note: 'G6', frequence: 1567.98 },
				{ note: 'G#6', frequence: 1661.22 },
				{ note: 'A6', frequence: 1760 },
				{ note: 'A#6', frequence: 1864.66 },
				{ note: 'B6', frequence: 1975.53 },
				{ note: 'C7', frequence: 2093 },
				{ note: 'C#7', frequence: 2217.46 },
				{ note: 'D7', frequence: 2349.32 },
				{ note: 'D#7', frequence: 2489.02 },
				{ note: 'E7', frequence: 2637.02 },
				{ note: 'F7', frequence: 2793.83 },
				{ note: 'F#7', frequence: 2959.96 },
				{ note: 'G7', frequence: 3135.96 },
				{ note: 'G#7', frequence: 3322.44 },
				{ note: 'A7', frequence: 3520 },
				{ note: 'A#7', frequence: 3729.31 },
				{ note: 'B7', frequence: 3951.07 },
				{ note: 'C8', frequence: 4186.01 }
		];

		for (let i in notes)
		{
			let note = notes[i];

			toutesLesNotes.push({
				note: note.note,
				note2: '',
				octave: 0,
				frequence: note.frequence,
				frequence_str: note.frequence.toFixed(2) + ' Hz'
			});
		}
				
		
			return toutesLesNotes;
		}
	}
	
}

</script>
