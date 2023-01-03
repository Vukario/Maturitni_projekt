<script
	src="https://web.archive.org/web/20201124004717js_/https://cdn.rawgit.com/google/code-prettify/master/loader/run_prettify.js"
>
	import Menu from '../lib/Menu.svelte';
	import Afinni from '../lib/Afinni_sifra.svelte';
	
</script>

<Menu />
<div class="main_page text-base">
	<Afinni/>
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
</div>

<div class="main_page text-base">
	
	
</div>

<style>
	.main_page {
		scroll-behavior: smooth;
		margin-left: 20%;
		margin-right: 2%;
	}
</style>
