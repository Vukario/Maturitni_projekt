<script>
// @ts-nocheck

import Prism from 'svelte-prism'
import Accordion from './Accordion.svelte'
import Test from './test.svelte';
import { Tabs, TabList, TabPanel, Tab } from './tabs.js'

let abc = "abcdefghijklmnopqrstuvwxyz";
let vysledek = new Array();
let kod = "kod";
let pocitadlo = 0;
let zprava = "ahooj jak se mas";
let zakod = "";
let pozice = 0;
let zacatek = 0;
let desifrace = "";
let krok = new Array();
let decipherPro = new Array();
let proslo = false;
let modKroky = false;
let kodik = [
		{ id: '0', name: `		for (let p = 0; p < zprava.length; p++) {` },
		{ id: '1', name: `		    if (zprava[p] !== " ") {` },
		{ id: '2', name: `			    zakod += vysledek[abc.indexOf(kod[pocitadlo])][abc.indexOf(zprava[p])];` },
    { id: '3', name: `			    pocitadlo += 1;` },
    { id: '4', name: `			    if (pocitadlo >= kod.length) {` },
    { id: '5', name: `			      pocitadlo = 0;` },
		{ id: '6', name: `				  }` },
		{ id: '7', name: `			  } else {` },
    { id: '8', name: `		      zakod += " ";` },
    { id: '9', name: `		    }` },
    { id: '10', name: `		}` },
	];


for (let i = 0; i < 26; i++) {
  vysledek.push([]);
  pozice = zacatek;
  for (let b = 0; b < 26; b++) {
    vysledek[i] += abc[pozice];
    pozice += 1;
    if (pozice > 25) {
      pozice = 0;
    }
  }
  zacatek += 1;
}
function ukoncitKrokovani(){
		proslo = false
		modKroky = false;
	}
	function handleClickModeKroky(){
		modKroky = true;
	}
    
function handleClick(){
//sifrovani
kod = kod.toLowerCase();
zprava = zprava.toLowerCase();
kod = kod.replaceAll(' ', '');
for (let index = 0; index < zprava.length; index++) {
      
			if (abc.includes(zprava[index])||zprava[index]==" ") {
               
			}else{
                
				zakod="chybný input";
				return;
            }
			
		}
for (let index = 0; index < kod.length; index++) {
      
			if (abc.includes(kod[index])||kod[index]==" ") {
               
			}else{
                
				zakod="chybný input";
				return;
            }
			
		}
  pocitadlo = 0;
  zakod = "";
  krok.push(0)
  decipherPro.push(zakod)
  krok.push(0)
  decipherPro.push(zakod) 
  for (let p = 0; p < zprava.length; p++) {
    krok.push(1)
    decipherPro.push(zakod) 
    if (zprava[p] !== " ") {
      
      zakod += vysledek[abc.indexOf(kod[pocitadlo])][abc.indexOf(zprava[p])];
      krok.push(2)
  decipherPro.push(zakod) 
      pocitadlo += 1;
      krok.push(3)
  decipherPro.push(zakod)
  krok.push(4)
  decipherPro.push(zakod) 
      if (pocitadlo >= kod.length) {
        krok.push(5)
  decipherPro.push(zakod) 
        pocitadlo = 0;
      }
    } else {
      krok.push(7)
  decipherPro.push(zakod) 
      zakod += " ";
      krok.push(8)
  decipherPro.push(zakod) 
    }
    krok.push(0)
  decipherPro.push(zakod) 
  }
  proslo = true;
  }
  function handleClick2(){
      //desifrovani
  pocitadlo = 0;
  zakod = "";
  console.log(vysledek[abc.indexOf(kod[pocitadlo])]);
  for (let x = 0; x < zprava.length; x++) {
    if (zprava[x] !== " ") {
      zakod += abc[vysledek[abc.indexOf(kod[pocitadlo])].indexOf(zprava[x])];
      pocitadlo += 1;
      if (pocitadlo >= kod.length) {
        pocitadlo = 0;
      }
    } else {
      zakod += " ";
    }
  }
}



console.log(zakod);
console.log(desifrace);

</script>


<link rel="stylesheet" href="/path/to/styles/default.min.css" />
<div class="py-8">
    
    <h1 class="text-7xl pb-8 ">Viegenova Šifra</h1>
    <p class="text-l pb-8">
      Vigenérova šifra je polyalfabetická substituční šifra, která k šifrování a dešifrování využívá tabula recta. Tabula recta obsahuje 26 pod sebou napsaných abeced. Na každém řádku začíná abeceda jiným písmenem. Na prvním řádku je abeceda napsaná standartně od a do z, druhý řádek je posunutý, písmena jsou zapsána od b do z následované písmenem a. Celý proces se opakuje pro každé písmeno. Klíčem pro Vigenèrovu šifru může být libovolné slovo. Při šifrování písmen se hledá ve sloupci každého písmena zprávy odpovídající písmeno ve sloupcích písmen klíče. Pro prvním písmeno zprávy se odpovídající písmeno hledá v řádku prvního písmena klíče. Tento proces se opakuje pro každé písmeno zprávy</p>
<p></p>
<label  for="text">Text k zašifrování</label>	
<textarea
class="block p-2.5 shadow appearance-none border rounded w-1/3	 py-2 my-5 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
name="text"
bind:value={zprava}
/>

<textarea
class="block p-2.5 shadow appearance-none border rounded w-1/3	 py-2 my-5 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
name="text"
bind:value={kod}
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
Dešifrovat
</button>

<h2 class="text-7xl pb-8 text-red-900">{zakod}</h2>
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
	
	
	<div class="w-full float-right pozadi rounded-lg">
		
		{#if modKroky}
		<Test cats={kodik} kroky={krok} postup={decipherPro}></Test>
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
let abc = "abcdefghijklmnopqrstuvwxyz";
let vysledek = new Array();
let kod = "kod";
let pocitadlo = 0;
let zprava = "ahooj jak se mas";
let zakod = "";
let pozice = 0;
let zacatek = 0;
for (let i = 0; i < 26; i++) { 
  vysledek.push([]);
  pozice = zacatek;
  for (let b = 0; b < 26; b++) {
    vysledek[i] += abc[pozice];
    pozice += 1;
    if (pozice > 25) {
      pozice = 0;
    }
  }
  zacatek += 1;
}
pocitadlo = 0;
zakod = "";
for (let p = 0; p < zprava.length; p++) {
  if (zprava[p]!== " ") {
    zakod += vysledek[abc.indexOf(kod[pocitadlo])][abc.indexOf(zprava[p])];
  pocitadlo += 1;

    if (pocitadlo >= kod.length) { 
	 //podmínka zajišťující 
      pocitadlo = 0;
    }
  } else {
    zakod += " "; 
  }
}
`}							
        </Prism>

    </TabPanel>

    <TabPanel>
        <Prism language="clike">
            {`
string abc = "abcdefghijklmnopqrstuvwxyz";
List<string> vysledek = new List<string>();
string kod = "kod";
int pocitadlo = 0;
string zprava = "ahooj jak se mas";
string zakod = "";
int pozice = 0;
int zacatek = 0;

for (int i = 0; i < 26; i++)
{
    vysledek.Add("");
    pozice = zacatek;
    for (int b = 0; b < 26; b++)
    {
        vysledek[i] += abc[pozice];
        pozice += 1;
        if (pozice > 25)
        {
            pozice = 0;
        }
    }
    zacatek += 1;
}

pocitadlo = 0;
zakod = "";

for (int p = 0; p < zprava.Length; p++)
{
    if (zprava[p] != ' ')
    {
        zakod += vysledek[abc.IndexOf(kod[pocitadlo])][abc.IndexOf(zprava[p])];
        pocitadlo += 1;
        if (pocitadlo >= kod.Length)
        {
            pocitadlo = 0;
        }
    }
    else
    {
        zakod += " ";
    }
}
Console.WriteLine(zakod);
Console.ReadLine();
            `}							
        </Prism>
    </TabPanel>
    
    <TabPanel>
        <Prism language="clike">
            {`
abc = "abcdefghijklmnopqrstuvwxyz"
vysledek = []
kod = "kod"
pocitadlo = 0
zprava = "ahoj jak se mas"
zakod = ""
pozice = 0
zacatek = 0

for i in range(26):
    vysledek.append("")
    pozice = zacatek
    for b in range(26):
        vysledek[i] += abc[pozice]
        pozice += 1
        if pozice > 25:
            pozice = 0
    zacatek += 1

pocitadlo = 0
zakod = ""

for p in range(len(zprava)):
    if zprava[p] != " ":
        zakod += vysledek[abc.index(kod[pocitadlo])][abc.index(zprava[p])]
        pocitadlo += 1
        if pocitadlo >= len(kod):
            pocitadlo = 0
    else:
        zakod += " "
print(zakod)
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
    
</svelte:head>
<style>
    .pozadi{
		background-color: rgb(245,242,240);
		
	}
	
    label {
  color: black;
  font-weight: bold;
  display: block;
}
label:after { content: ": " }
</style>