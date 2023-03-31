<script>
// @ts-nocheck

import Prism from 'svelte-prism'
import Accordion from './Accordion.svelte'
import Test from './test.svelte';
import { Tabs, TabList, TabPanel, Tab } from './tabs.js'


let string =
"010203040506070809101112131415161718192021222324252627282930313233343536373839404142434445464748495051525354555657585960616263646566676869707172737475767778798081828384858687888990919293949596979899";
let pole = string.match(/..?/g);

let homophones = new Array();

let cislo = 99;
let rng;
let abc = "abcdefghijklmnopqrstuvwxyz";
let message = "Ahoj";
let encrypted = "";
let krok = new Array();
let decipherPro = new Array();
let proslo = false;
let modKroky = false;
let kod = [
		{ id: '0', name: `		encrypted = "";` },
		{ id: '1', name: `		for (let i = 0; i < message.length; i++) {` },
		{ id: '2', name: `			const letter = message[i].toLowerCase();` },
        { id: '3', name: `			if (letter !== " ") {` },
        { id: '4', name: `			const homophoneIndex = Math.floor(Math.random() * homophones[abc.indexOf(letter)].length);` },
        { id: '5', name: `			encrypted += homophones[abc.indexOf(letter)][homophoneIndex];` },
		{ id: '6', name: `			} else {` },
		{ id: '7', name: `			encrypted += message[i];` },
        { id: '8', name: `		    }` },
        { id: '9', name: `		}` },
	];



for (let a = 0; a < 26; a++) {
  homophones.push([]);
  for (let b = 0; b < 3; b++) {
    rng = Math.floor(Math.random() * cislo);

    homophones[a].push(pole[rng]);
  
    pole.splice(rng, 1);
    cislo = cislo - 1;
  }
}
console.log(homophones);


function ukoncitKrokovani(){
		proslo = false
		modKroky = false;
	}
	function handleClickModeKroky(){
		modKroky = true;
	}	

function handleClick() {
    message = message.toLowerCase();

    for (let index = 0; index < message.length; index++) {
      
			if (abc.includes(message[index])||message[index]==" ") {
               
			}else{
                
				encrypted="chybný input";
				return;
            }
			
		}
    krok.push(0)
	decipherPro.push(encrypted)    
encrypted = "";
    krok.push(1)
	decipherPro.push(encrypted)  
  for (let i = 0; i < message.length; i++) {
    krok.push(2)
	decipherPro.push(encrypted)  
    const letter = message[i].toLowerCase();
    krok.push(3)
	decipherPro.push(encrypted)  
    if (letter !== " ") {
        krok.push(4)
	    decipherPro.push(encrypted)  
      const homophoneIndex = Math.floor(Math.random() * homophones[abc.indexOf(letter)].length);
      
      encrypted += homophones[abc.indexOf(letter)][homophoneIndex];
      krok.push(5)
	    decipherPro.push(encrypted)  
      krok.push(1)
	  decipherPro.push(encrypted)  
    } else {
        krok.push(6)
	decipherPro.push(encrypted)
 
      encrypted += message[i];
      krok.push(7)
	decipherPro.push(encrypted) 
      krok.push(1)
	decipherPro.push(encrypted)  
    }
  }
  console.log(encrypted);
  proslo = true;
}

function handleClick2() {
  encrypted = '';
  for (let i = 0; i < (message.length + message.split(' ').length - 1)/2; i++) {
    const homophonesArray = Object.values(homophones).flat();
    console.log(homophonesArray)
    // @ts-ignore
    const homophoneIndex = homophonesArray.indexOf(message.match(/ |..?/g)[i]);
    if (homophoneIndex !== -1) {
      const letterIndex = Math.floor(homophoneIndex / 3);
      encrypted += abc[letterIndex];
    } else {
    
      encrypted += " ";
    }
    console.log(encrypted);
  }

}


</script>


    <link rel="stylesheet" href="/path/to/styles/default.min.css" />
    <div class="py-8">
        
        <h1 class="text-7xl pb-8 ">Homofonní Šifra</h1>
        <p class="text-l pb-8">
            Homofonní šifra patří mezi pokročilejší substituční šifry. Využívá nahrazování jednotlivých písmen abecedy za několik různých symbolů nebo kombinací symbolů. Tyto nahrazování jsou obvykle vytvořeny tak, aby každé písmeno mělo mnoho možných kombinací, a tím pádem je těžké zjistit, jaké písmeno nebo kombinace písmen daný symbol představuje. Homofonní šifry mohou být vytvářeny různými způsoby. Některé šifry nahrazují jednotlivá písmena za jediný symbol nebo kombinaci symbolů, zatímco jiné šifry používají různé symboly a kombinace pro každou jednotlivou pozici v textu. Tyto různé přístupy mají různé úrovně zabezpečení a složitosti. Pro vytvoření homofonní šifry je obvykle nutné mít klíč, který umožní převést šifrovaný text zpět do původního textu. Tento klíč obsahuje informace o tom, které symboly odpovídají jednotlivým písmenům abecedy. Bez klíče je dešifrování velmi obtížné a v některých případech nemožné.</p>
    <p></p>
    <label  for="text">Text k zašifrování</label>	
    <textarea
    class="block p-2.5 shadow appearance-none border rounded w-1/3	 py-2 my-5 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
    name="text"
    bind:value={message}
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

    <h2 class="text-7xl pb-8 text-red-900">{encrypted}</h2>
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
            
        </TabList>
    
        <TabPanel>
        
            <Prism language="javascript">
                {`
    let cislo = 99;
    let rng;
    let abc = "abcdefghijklmnopqrstuvwxyz";
    let message = "Ahoj";
    let encrypted = "";
    for (let a = 0; a < 26; a++) {
    homophones.push([]);
    for (let b = 0; b < 3; b++) {
        rng = Math.floor(Math.random() * cislo);
        homophones[a].push(pole[rng]);
        pole.splice(rng, 1);
        cislo = cislo - 1;
    }
    }
    console.log(homophones);




    function encription() {
    encrypted = "";
    for (let i = 0; i < message.length; i++) {
        const letter = message[i].toLowerCase();
        if (letter !== " ") {

        const homophoneIndex = Math.floor(Math.random() * homophones[abc.indexOf(letter)].length);
        encrypted += homophones[abc.indexOf(letter)][homophoneIndex];
        } else {
        encrypted += message[i];
        }
    }
    
    }

    function decription() {
    encrypted = '';
    for (let i = 0; i < (message.length + message.split(' ').length - 1)/2; i++) {
        const homophonesArray = Object.values(homophones).flat();
        console.log(homophonesArray)
        const homophoneIndex = homophonesArray.indexOf(message.match(/ |..?/g)[i]);
        if (homophoneIndex !== -1) {
        const letterIndex = Math.floor(homophoneIndex / 3);
        encrypted += abc[letterIndex];
        } else {
        
        encrypted += " ";
        }
        console.log(encrypted);
    }

    } `}							
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