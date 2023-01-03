<script>
// @ts-nocheck

	
	
	import Prism from 'svelte-prism'

	import { Tabs, TabList, TabPanel, Tab } from './tabs.js'
	

	let number = 0;
	let helper = 0;
	let string = 'ahoj';
	let vysledek = 'ahoj';
	let abcd = 'abcdefghijklmnopqrstuvwxyz'
	
	//check if letter is uppercase


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
			helper = abcd.indexOf(str[i]) ;
			console.log(helper);
			helper += parseInt(key);
			console.log(helper);
			if (helper > 25) {
				helper = helper - 26
			}
			decipher = decipher + abcd.charAt(helper);
			
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
		bind:value={number}
	/>
	<button
		class="bg-transparent hover:bg-stone-900 text-stone-900 font-semibold hover:text-white py-2 px-4 border border-stone-900 hover:border-transparent rounded"
		on:click={handleClick}
	>
		Šifrovat
	</button>
	<h2 class="text-7xl pb-8 text-red-900">{vysledek}</h2>

	<Tabs>
		<TabList>
			<Tab>JS</Tab>
			<Tab>c#</Tab>
			<Tab>python</Tab>
		</TabList>

		<TabPanel>
			<!-- <pre><code class="language-javascript">
				
				nuber = 0;
				let string = 'ahoj';
				let vysledek = 'ahoj';
				function isUpperCase(str) &#123
					return str === str.toUpperCase();
				&#125
			</code></pre> -->
			<Prism language="javascript">
				{`
	let nuber = 0;
	let string = 'ahoj';
	let vysledek = 'ahoj';
	//check if letter is uppercase
	function isUpperCase(str) {
		return str === str.toUpperCase();
	}
	function handleClick() {
		ceaserCipher(string, nuber);
	}
	//decipher the string
	let ceaserCipher = (str, key) => {
		let decipher = '';

		//decipher each letter
		for (let i = 0; i < str.length; i++) {
			//if letter is uppercase then add uppercase letters
			if (isUpperCase(str[i])) {
				decipher += String.fromCharCode(((str.charCodeAt(i) + key - 65) % 26) + 65);
			} else {
				//else add lowercase letters
				decipher += String.fromCharCode(((str.charCodeAt(i) + key - 97) % 26) + 97);
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

print(cezar_cyper("hello world", 3)) # "khoor zruog"
print(cezar_cyper("hello world", 7)) # "olssv dvysk"
print(cezar_cyper("hello world", 11)) # "wrrrm jgtgt"
				`}							
			</Prism>
		</TabPanel>
	</Tabs>
</div>

<svelte:head>
	<link
		href="https://cdnjs.cloudflare.com/ajax/libs/prism/1.22.0/themes/prism.min.css"
		rel="stylesheet"
	/>
</svelte:head>
