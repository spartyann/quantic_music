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
				{ note: 'A0', octave: 0, frequence: 27.5 },
				{ note: 'A#0', octave: 0, frequence: 29.14 },
				{ note: 'B0', octave: 0, frequence: 30.87 },
				{ note: 'C1', octave: 1, frequence: 32.7 },
				{ note: 'C#1', octave: 1, frequence: 34.65 },
				{ note: 'D1', octave: 1, frequence: 36.71 },
				{ note: 'D#1', octave: 1, frequence: 38.89 },
				{ note: 'E1', octave: 1, frequence: 41.2 },
				{ note: 'F1', octave: 1, frequence: 43.65 },
				{ note: 'F#1', octave: 1, frequence: 46.25 },
				{ note: 'G1', octave: 1, frequence: 49 },
				{ note: 'G#1', octave: 1, frequence: 51.96 },
				{ note: 'A1', octave: 1, frequence: 55 },
				{ note: 'A#1', octave: 1, frequence: 58.27 },
				{ note: 'B1', octave: 1, frequence: 61.74 },
				{ note: 'C2', octave: 2, frequence: 65.41 },
				{ note: 'C#2', octave: 2, frequence: 69.3 },
				{ note: 'D2', octave: 2, frequence: 73.42 },
				{ note: 'D#2', octave: 2, frequence: 77.78 },
				{ note: 'E2', octave: 2, frequence: 82.41 },
				{ note: 'F2', octave: 2, frequence: 87.31 },
				{ note: 'F#2', octave: 2, frequence: 92.5 },
				{ note: 'G2', octave: 2, frequence: 98 },
				{ note: 'G#2', octave: 2, frequence: 103.83 },
				{ note: 'A2', octave: 2, frequence: 110 },
				{ note: 'A#2', octave: 2, frequence: 116.54 },
				{ note: 'B2', octave: 2, frequence: 123.47 },
				{ note: 'C3', octave: 3, frequence: 130.81 },
				{ note: 'C#3', octave: 3, frequence: 138.59 },
				{ note: 'D3', octave: 3, frequence: 146.83 },
				{ note: 'D#3', octave: 3, frequence: 155.56 },
				{ note: 'E3', octave: 3, frequence: 164.81 },
				{ note: 'F3', octave: 3, frequence: 174.61 },
				{ note: 'F#3', octave: 3, frequence: 185 },
				{ note: 'G3', octave: 3, frequence: 196 },
				{ note: 'G#3', octave: 3, frequence: 207.65 },
				{ note: 'A3', octave: 3, frequence: 220 },
				{ note: 'A#3', octave: 3, frequence: 233.08 },
				{ note: 'B3', octave: 3, frequence: 246.94 },
				{ note: 'C4', octave: 4, frequence: 261.63 },
				{ note: 'C#4', octave: 4, frequence: 277.18 },
				{ note: 'D4', octave: 4, frequence: 293.66 },
				{ note: 'D#4', octave: 4, frequence: 311.13 },
				{ note: 'E4', octave: 4, frequence: 329.63 },
				{ note: 'F4', octave: 4, frequence: 349.23 },
				{ note: 'F#4', octave: 4, frequence: 369.99 },
				{ note: 'G4', octave: 4, frequence: 392 },
				{ note: 'G#4', octave: 4, frequence: 415.3 },
				{ note: 'A4', octave: 4, frequence: 440 },
				{ note: 'A#4', octave: 4, frequence: 466.16 },
				{ note: 'B4', octave: 4, frequence: 493.88 },
				{ note: 'C5', octave: 5, frequence: 523.25 },
				{ note: 'C#5', octave: 5, frequence: 554.37 },
				{ note: 'D5', octave: 5, frequence: 587.33 },
				{ note: 'D#5', octave: 5, frequence: 622.25 },
				{ note: 'E5', octave: 5, frequence: 659.25 },
				{ note: 'F5', octave: 5, frequence: 698.46 },
				{ note: 'F#5', octave: 5, frequence: 739.99 },
				{ note: 'G5', octave: 5, frequence: 783.99 },
				{ note: 'G#5', octave: 5, frequence: 830.61 },
				{ note: 'A5', octave: 5, frequence: 880 },
				{ note: 'A#5', octave: 5, frequence: 932.33 },
				{ note: 'B5', octave: 5, frequence: 987.77 },
				{ note: 'C6', octave: 6, frequence: 1046.5 },
				{ note: 'C#6', octave: 6, frequence: 1108.73 },
				{ note: 'D6', octave: 6, frequence: 1174.66 },
				{ note: 'D#6', octave: 6, frequence: 1244.51 },
				{ note: 'E6', octave: 6, frequence: 1318.51 },
				{ note: 'F6', octave: 6, frequence: 1396.91 },
				{ note: 'F#6', octave: 6, frequence: 1479.98 },
				{ note: 'G6', octave: 6, frequence: 1567.98 },
				{ note: 'G#6', octave: 6, frequence: 1661.22 },
				{ note: 'A6', octave: 6, frequence: 1760 },
				{ note: 'A#6', octave: 6, frequence: 1864.66 },
				{ note: 'B6', octave: 6, frequence: 1975.53 },
				{ note: 'C7', octave: 7, frequence: 2093 },
				{ note: 'C#7', octave: 7, frequence: 2217.46 },
				{ note: 'D7', octave: 7, frequence: 2349.32 },
				{ note: 'D#7', octave: 7, frequence: 2489.02 },
				{ note: 'E7', octave: 7, frequence: 2637.02 },
				{ note: 'F7', octave: 7, frequence: 2793.83 },
				{ note: 'F#7', octave: 7, frequence: 2959.96 },
				{ note: 'G7', octave: 7, frequence: 3135.96 },
				{ note: 'G#7', octave: 7, frequence: 3322.44 },
				{ note: 'A7', octave: 7, frequence: 3520 },
				{ note: 'A#7', octave: 7, frequence: 3729.31 },
				{ note: 'B7', octave: 7, frequence: 3951.07 },
				{ note: 'C8', octave: 8, frequence: 4186.01 }
		];

		
		let cCurrentNote = 0;

		for (let i in notes)
		{
			let note = notes[i];

			note.note2 = noms2DeNotes[cCurrentNote] + note.octave
			
			cCurrentNote++;
			if (cCurrentNote > 11) { cCurrentNote = 0}

			toutesLesNotes.push({
				note: note.note,
				note2: note.note2,
				octave: note.octave,
				frequence: note.frequence,
				frequence_str: note.frequence.toFixed(2) + ' Hz'
			});
		}
				
		
			return toutesLesNotes;
		}
	}
	
}

</script>
