<script>
// @ts-nocheck

	
	import Accordion from './Accordion.svelte'
	import Prism from 'svelte-prism'
	import Test from './test.svelte';
	import { Tabs, TabList, TabPanel, Tab } from './tabs.js'
	
	
	let number = 0;
	let helper = 0;
	let proslo = false;
	let modKroky = false;
	let string = 'ahoj';
	let vysledek = 'ahoj';
	let abcd = 'abcdefghijklmnopqrstuvwxyz'
	let krok = new Array();
	let decipherPro = new Array();
	let kod = [
		{ id: '1', name: `		let decipher = '';` },
		{ id: '2', name: `		str = str.toLowerCase();` },
		{ id: '3', name: `		for (let i = 0; i < str.length; i++) {` },
        { id: '4', name: `			if (str[i]==' ') {` },
        { id: '5', name: `				decipher += ' ';` },
        { id: '6', name: `			} else {` },
		{ id: '7', name: `				helper = abcd.indexOf(str[i]) ;` },
		{ id: '8', name: `				helper += parseInt(key);` },
        { id: '9', name: `				if (helper > 25) {` },
        { id: '10', name: `					helper = helper - 26` },
        { id: '11', name: `				}` },
		{ id: '12', name: `				decipher = decipher + abcd.charAt(helper);` },
        { id: '13', name: `			}` },
        { id: '14', name: `		}` },
        { id: '15', name: `		vysledek = decipher;` },
        { id: '16', name: `		return decipher;` }
	];


	function ukoncitKrokovani(){
		proslo = false
		modKroky = false;
	}
	function handleClickModeKroky(){
		modKroky = true;
	}
	function handleClick() {
		ceaserCipher(string, number);
		
	}
	
	function handleClick2() {
		ceaserDeCipher(string, number);
	}
	//decipher the string
	let ceaserDeCipher = (str, key) =>{
		let decipher = '';
		
		str = str.toLowerCase();
		for (let i = 0; i < str.length; i++) {
			if (str[i]==' ') {
				decipher += ' ';
			} else {
				helper = abcd.indexOf(str[i]) ;
				console.log(helper);
				helper -= parseInt(key);
				console.log(helper);

				if (helper < 0) {

					helper = helper + 26
				}

				decipher = decipher + abcd.charAt(helper);
			}
			
			
		}
		vysledek = decipher;
		console.log(vysledek);
		return decipher;

	}
	let ceaserCipher = (str, key) => {
		
		
		let decipher = '';
		krok.push(0)
		decipherPro.push(decipher)
		krok.push(1)
		decipherPro.push(decipher)
		krok.push(2)
		decipherPro.push(decipher)
		str = str.toLowerCase();
		krok.push(3)
		decipherPro.push(decipher)
		for (let i = 0; i < str.length; i++) {
		krok.push(4)
		decipherPro.push(decipher)
			if (str[i]==' ') {
				decipher += ' ';
				krok.push(5)
				decipherPro.push(decipher)

				krok.push(3)
				decipherPro.push(decipher)
			} else {
				krok.push(6)
				decipherPro.push(decipher)

				helper = abcd.indexOf(str[i]);
				krok.push(7)
				decipherPro.push(decipher)

				helper += parseInt(key);
				krok.push(8)
				decipherPro.push(decipher)

				krok.push(9)
				decipherPro.push(decipher)

				if (helper > 25) {
					krok.push(10)
					decipherPro.push(decipher)
					helper = helper - 26
				}
				

				decipher = decipher + abcd.charAt(helper);
				krok.push(12)
				decipherPro.push(decipher)
				
				krok.push(3)
				decipherPro.push(decipher)
			}
			
			
		}
		vysledek = decipher;
		krok.push(15)
		decipherPro.push(decipher)
		krok.push(16)
		decipherPro.push(decipher)
		console.log(vysledek);
		console.log(krok);
		console.log(decipherPro);
		proslo = true;
		return decipher;
	};
</script>

<link rel="stylesheet" href="/path/to/styles/default.min.css" />
<div class="py-8">
	<div class="">
	<h1 class="text-7xl pb-8 ">Caesarova šifra</h1>
	<p class="text-l pb-8 ">
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
	
	<div class="w-2/5 omyl">
	<label  for="text">Text k zašifrování</label>	
	<textarea
	class="block p-2.5 shadow appearance-none border rounded w-full py-2 my-5 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
	name="text"
	bind:value={string}
	/>
	<label  for="key">Klíč</label>
	<input
		class="shadow appearance-none border rounded w-15 my-5 py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
		name="key"
		bind:value={number}
	/>
	<button
		class="bg-transparent hover:bg-stone-900 text-stone-900 font-semibold hover:text-white py-2 px-4 border border-stone-900 hover:border-transparent rounded"
		on:click={handleClick}
	>
		Šifrovat
	</button>
	<button
		class="bg-transparent hover:bg-stone-900 text-stone-900 font-semibold hover:text-white py-2 px-4 border border-stone-900 hover:border-transparent rounded"
		on:click={handleClick2}
	>
		Rozšifrovat
	</button>
	{#if proslo}
		
	
	<button
		class="bg-transparent hover:bg-stone-900 text-stone-900 font-semibold hover:text-white py-2 px-4 border border-stone-900 hover:border-transparent rounded"
		on:click={handleClickModeKroky}
	>
		krokování
	</button>
	{/if}
	{#if modKroky}
	<button
		class="bg-transparent hover:bg-stone-900 text-stone-900 font-semibold hover:text-white py-2 px-4 border border-stone-900 hover:border-transparent rounded"
		on:click={ukoncitKrokovani}
	>
		ukončit krokování
	</button>
	{/if}
	<h2 class="text-7xl text-red-900">{vysledek}</h2>
	</div>
	<div class="w-full float-right dick rounded-lg">
		
		{#if modKroky}
		<Test cats={kod} kroky={krok} postup={decipherPro}></Test>
		{/if}
	
	</div>
	{#if modKroky == false}
	<Accordion>
		<span slot="head">Ukázat kód</span>
		<div slot="details">
			<Tabs>
				<TabList>
					<Tab>JS</Tab>
					<Tab>c#</Tab>
					<Tab>python</Tab>
				</TabList>
		
				<TabPanel>
					<Prism language="javascript">
						
		
						{`
			let number = 0;
			let helper = 0;
			let string = 'ahoj';
			let vysledek = 'ahoj';
			let abcd = 'abcdefghijklmnopqrstuvwxyz'
			
			
		
		
			function handleClick() {
				ceaserCipher(string, number);
			}
			//decipher the string
			let ceaserCipher = (str, key) => {
				let decipher = '';
				console.log(str);
				str = str.toLowerCase();
				console.log(str);
				//decipher each letter
				for (let i = 0; i < str.length; i++) {
					if (str[i]==' ') {
						decipher += ' ';
					} else {
						helper = abcd.indexOf(str[i]) ;
						console.log(helper);
						helper += parseInt(key);
						console.log(helper);
						
						if (helper > 25) {
		
							helper = helper - 26
						}
		
						decipher = decipher + abcd.charAt(helper);
					}
					
					
				}
				vysledek = decipher;
				console.log(vysledek);
				return decipher;
			};
						`}							
					</Prism>
		
				</TabPanel>
		
				<TabPanel>
					<Prism language="clike">
						{`
		using System;
		using System.Linq;
		
		namespace CaesarCipher
		{
			class Program
			{
				static void Main(string[] args)
				{
					Console.Write("Enter a message to encrypt: ");
					string message = Console.ReadLine();
		
					Console.Write("Enter a key (1-26): ");
					int key = int.Parse(Console.ReadLine());
		
					string encryptedMessage = Encrypt(message, key);
					Console.WriteLine($"Encrypted message: {encryptedMessage}");
		
					string decryptedMessage = Decrypt(encryptedMessage, key);
					Console.WriteLine($"Decrypted message: {decryptedMessage}");
				}
		
				static string Encrypt(string message, int key)
				{
					char[] encrypted = message.ToLower().ToCharArray().Select(c =>
					{
						if (!char.IsLetter(c))
						{
							return c;
						}
		
						char letter = (char)(c + key);
		
						if (letter > 'z')
						{
							return (char)(letter - 26);
						}
		
						return letter;
					}).ToArray();
		
					return new string(encrypted);
				}
		
				static string Decrypt(string message, int key)
				{
					return Encrypt(message, 26 - key);
				}
			}
		}
						`}							
					</Prism>
				</TabPanel>
				
				<TabPanel>
					<Prism language="clike">
						
						{`
		def cezar_cyper(plaintext, shift):
		 cyphertext = ""
		 for i in plaintext:
		  if i.isalpha():
		   cyphertext += chr((ord(i) - ord('a') + shift) % 26 + ord('a'))
		  else:
		   cyphertext += i
		 return cyphertext
		
		print(cezar_cyper("hello world", 0)) # "khoor zruog"
		print(cezar_cyper("hello world", 7)) # "olssv dvysk"
		print(cezar_cyper("hello world", 11)) # "wrrrm jgtgt"
						`}							
					</Prism>
				</TabPanel>
			</Tabs>
		</div>
	</Accordion>
	{/if}
	
</div>

<svelte:head>
	<link
		href="https://cdnjs.cloudflare.com/ajax/libs/prism/1.22.0/themes/prism.min.css"
		rel="stylesheet"
	/>
	<script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
  <script id="MathJax-script" async
          src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js">
  </script>
</svelte:head>
<style>
	.dick{
		background-color: rgb(245,242,240);
		
	}
	.omyl{
		padding-bottom: 10rem;
	}
	label {
  color: black;
  font-weight: bold;
  display: block;
}
label:after { content: ": " }
</style>