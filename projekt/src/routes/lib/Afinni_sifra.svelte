<script>


// @ts-nocheck


let b = 0;
let a = 0;
let helper = 0;
let string = 'ahoj';
let vysledek = 'ahoj';
let abcd = 'abcdefghijklmnopqrstuvwxyz'


	function handleClick() {
		afinniCipher(string, a , b);
	}
	
	let afinniCipher = (str, a, b) => {
		let decipher = '';

		
		for (let i = 0; i < str.length; i++) {
            helper = (parseInt(a)*abcd.indexOf(str[i]) + parseInt(b)) % 26;
			decipher += abcd.charAt(helper)
		}
		vysledek = decipher;
		console.log(vysledek);
		return decipher;
	};
</script>

<link rel="stylesheet" href="/path/to/styles/default.min.css" />
<div class="py-8">
	
	<h1 class="text-7xl pb-8 ">Cezarova šifra</h1>
	<p class="text-l pb-8">
		Princip Caesarovy šifry je založen na tom, že všechna písmena zprávy jsou během šifrování
		zaměněna za písmeno,které se abecedně nachází o pevně určený počet míst dále (tj. posun je
		pevně zvolen). Počet možných variant klíče této šifry je o jedna menší než počet písmen (znaků)
		v použité abecedě. Zvolíme-li hodnotu posunu stejnou, jako je počet znaků použité abecedy, bude
		zašifrovaná zpráva identická s předlohou. Vyšším posunem, například posunem s klíčem o jedna
		větší, než je počet písmen (znaků) abecedy, dostaneme zašifrovanou zprávu odpovídající prostému
		posunu o klíč jedna, takže použití klíče hodnoty vyšší než počet znaků abecedy nemá
		kryptografický význam. V některých pramenech se proto o Caesarových šifrách mluví jako o šifrách
		aditivních. Na stejném principu také funguje Vigenèrova šifra, pouze místo jedné šifrové abecedy
		používá 26 šifrových abeced, čímž dosahuje vyšší kvality šifrování.
	</p>

<input 
class="shadow appearance-none border rounded w-15 py-2 my-5 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
bind:value={string}
/>

<input
class="shadow appearance-none border rounded w-15 my-5 py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
bind:value={a}
/>
<input
class="shadow appearance-none border rounded w-15 my-5 py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
bind:value={b}
/>
<button
class="bg-transparent hover:bg-stone-900 text-stone-900 font-semibold hover:text-white py-2 px-4 border border-stone-900 hover:border-transparent rounded"
on:click={handleClick}
>
Šifrovat
</button>
<h2 class="text-7xl pb-8 text-red-900">{vysledek}</h2>
</div>