<script>


    // @ts-nocheck
    import Prism from 'svelte-prism'
import Accordion from './Accordion.svelte'
import Test from './test.svelte';
import { Tabs, TabList, TabPanel, Tab } from './tabs.js'
    
    let sifra = '';
    let limit = 0;
    let key = 3;            
    let tabulka = new Array();
    let vypis ='';
    let decipher = new Array();
    let krok = new Array();
    let decipherPro = new Array();
    let proslo = false;
    let modKroky = false;
    let kod = [
		{ id: '0', name: `		for (let i = 0; i < Math.ceil(sifra.length/key); i++) {` },
		{ id: '1', name: `		    if (limit<sifra.length) {` },
		{ id: '2', name: `			    tabulka.push(sifra[limit]);` },
        { id: '3', name: `			    limit += 1;` },
        { id: '4', name: `			}` },
        { id: '5', name: `			for (let x = 0; x < key-1; x++) {` },
		{ id: '6', name: `				if (limit<sifra.length) {` },
		{ id: '7', name: `			        tabulka[i]+=sifra[limit]` },
        { id: '8', name: `		            limit += 1;` },
        { id: '9', name: `		        }` },
        { id: '10', name: `			}` },
		{ id: '11', name: `		}` },
        { id: '12', name: `		for (let i = 0; i < key; i++) {` },
        { id: '13', name: `		    decipher.push('');` },
        { id: '14', name: `		}` },
		{ id: '15', name: `		for (let index = 0; index < key; index++) {` },
        { id: '16', name: `		   for (let i = 0; i < Math.ceil(sifra.length/key); i++) {` },
        { id: '17', name: `		        if(typeof tabulka[i][index] !== 'undefined'){` },
        { id: '18', name: `		            decipher[index] += tabulka[i][index]` },
		{ id: '19', name: `		        }` },
        { id: '20', name: `		   }` },
        { id: '21', name: `		}` },
        { id: '22', name: `		for (let index = 0; index < decipher.length; index++) {` },
        { id: '23', name: `		   vypis += decipher[index];` },
        { id: '24', name: `		}` },
        
	];

    function ukoncitKrokovani(){
		proslo = false
		modKroky = false;
	}
	function handleClickModeKroky(){
		modKroky = true;
	}
    
        function handleClick() {
            traspozicniSifra();
        }

        let traspozicniSifra = () => {
        
        if (parseInt(key) || key == 0) {
			
		}else{
			vypis="klíč musí být číslo";
				return;
		}
        if(key<2){
            return;
        }    
       
        limit = 0;      
        tabulka = new Array();
        vypis ='';
        decipher = new Array();    
       
        

        sifra = sifra.replaceAll(' ', '');
        krok.push(0)
		decipherPro.push("")
        krok.push(0)
		decipherPro.push("")
        for (let i = 0; i < Math.ceil(sifra.length/key); i++) {
            krok.push(1)
		    decipherPro.push("")
                if (limit<sifra.length) {
                    krok.push(2)
		            decipherPro.push("")    
   
                    tabulka.push(sifra[limit]);
                    krok.push(3)
		            decipherPro.push("")
                    limit += 1;
                }
                krok.push(5)
		        decipherPro.push("")
               for (let x = 0; x < key-1; x++) {
                krok.push(6)
		        decipherPro.push("")
                if (limit<sifra.length) {
                    krok.push(7)
		            decipherPro.push("")
                    tabulka[i]+=sifra[limit]
                    krok.push(8)
		            decipherPro.push("")
                    limit += 1;
                }
                krok.push(5)
		        decipherPro.push("")
               }
               krok.push(0)
		    decipherPro.push("")
            }
            
        krok.push(12)
	    decipherPro.push("")
        for (let i = 0; i < key; i++) {
            krok.push(13)
		    decipherPro.push("")
            decipher.push('');
            krok.push(12)
		    decipherPro.push("")
           }
        krok.push(15)
		decipherPro.push("")
        for (let index = 0; index < key; index++) {
            krok.push(16)
		    decipherPro.push("")
           for (let i = 0; i < Math.ceil(sifra.length/key); i++) {
            krok.push(17)
		    decipherPro.push("")
                if(typeof tabulka[i][index] !== 'undefined'){
                    krok.push(18)
		            decipherPro.push("")
                    decipher[index] += tabulka[i][index]
                    krok.push(18)
		            decipherPro.push("")
                }
                krok.push(16)
		    decipherPro.push("")
           }
           krok.push(15)
		    decipherPro.push("")
        }
        krok.push(22)
		decipherPro.push("")
        for (let index = 0; index < decipher.length; index++) {
            krok.push(23)
		    decipherPro.push("")
           vypis += decipher[index];
           krok.push(22)
		    decipherPro.push("")
        }
        proslo = true;
        };

    </script>
    
    <link rel="stylesheet" href="/path/to/styles/default.min.css" />
    <div class="py-8">
        
        <h1 class="text-7xl pb-8 ">Transpoziční šifra</h1>
        <p class="text-l pb-8">
            Transpoziční šifra je druh šifry, který se zaměřuje na přeskupení písmen v zašifrovaném textu na základě předem domluveného systému. Šifrování probíhá postupný zapsáním tajné zprávy do tabulky. Počet sloupců je dán předem domluveným klíčem. První tabulku následně po sloupcích přepíšete do nové. Velkou výhodou transpoziční šifry je její jednoduchost. K šifrování a rozšifrování není zapotřebí žádné matematiky. Takže to zvládne téměř každý.</p>
    <p></p>
    
    <label  for="text">Text k zašifrování</label>	
    <textarea
    class="block p-2.5 shadow appearance-none border rounded w-1/3	 py-2 my-5 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
    name="text"
    bind:value={sifra}
    />
    
    <label class="mt-10"  for="valueA">Zadej klíč</label>
<input
class="shadow appearance-none border rounded w-15 my-5 py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
name="valueA"
bind:value={key}
/>

    <button
    class="bg-transparent hover:bg-stone-900 text-stone-900 font-semibold hover:text-white py-2 px-4 border border-stone-900 hover:border-transparent rounded"
    on:click={handleClick}
    >
    Šifrovat
    </button>

    <h2 class="text-7xl pb-8 text-red-900">{vypis}</h2>
    <div class="h-fit">
   
        {#each tabulka as table}
        <tr >
            {#each Array.from(table) as cat}
                <th class="border-2 p-2">
                    {cat}
                </th>
            {/each}
        </tr>
        
        {/each}
        <div class="pb-1"></div>
        {#each decipher as table}
        <tr>
            {#each Array.from(table) as cat}
                <th class="border-2 p-2">
                    {cat}
                </th>
            {/each}
        </tr>
        
        {/each}
        <div class="pb-1"></div>
    </div>
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
        let sifra = '';
        let limit = 0;
        let key = 3;            
        let tabulka = new Array();
        let vypis ='';
        let decipher = new Array();
    
        let traspozicniSifra = () => {
        if(key<2){
            return;
        }    
        
        limit = 0;      
        tabulka = new Array();
        vypis ='';
        decipher = new Array();    
       
        
        console.log(Math.ceil(sifra.length/key));
        sifra = sifra.replaceAll(' ', '');
        console.log(sifra.length);
        console.log(Math.ceil(sifra.length/key));
        for (let i = 0; i < Math.ceil(sifra.length/key); i++) {
                if (limit<sifra.length) {
   
                    tabulka.push(sifra[limit]);
                    limit += 1;
                }
               for (let x = 0; x < key-1; x++) {
                if (limit<sifra.length) {
                    tabulka[i]+=sifra[limit]
                    limit += 1;
                }
               } 
            }
            
     
        for (let i = 0; i < key; i++) {
            
            decipher.push('');
            
           }
        for (let index = 0; index < key; index++) {
            
           
           for (let i = 0; i < Math.ceil(sifra.length/key); i++) {
                if(typeof tabulka[i][index] !== 'undefined'){
                    decipher[index] += tabulka[i][index]
                }

               
           }
            
        }
        for (let index = 0; index < decipher.length; index++) {
           vypis += decipher[index];
            
        }
        console.log(decipher);
        console.log(vypis);
        
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
        .bottom {
    position: absolute;
    bottom: 0;
    right: 0; /* set the right to 0 */
  }
  

        label:after { content: ": " }
        </style>