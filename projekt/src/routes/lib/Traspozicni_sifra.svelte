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
                <Tab>c#</Tab>
                
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
    List<List<char>> tabulka = new List<List<char>>();
    Console.WriteLine("zadej text k zašifrování");
    string text = Convert.ToString(Console.ReadLine());
    Console.WriteLine("zadej klíč");
    double key = Convert.ToInt32(Console.ReadLine());
    int pocitadlo = 0;
    string zas = "";
    text = text.Replace(" ", "");


    for (int i = 0; i < Math.Ceiling(text.Length / key); i++)
    {
        tabulka.Add(new List<char>());
        for (int x = 0; x < key; x++)
        {
            if (pocitadlo >= text.Length)
            {
                break;
            }
            tabulka[i].Add(text[pocitadlo]);
            pocitadlo++;

        }
    }

    foreach (var item in tabulka)
    {
        foreach (var vypis in item)
        {
            Console.Write(vypis);
        }
        Console.WriteLine();
    }
    Console.ReadLine();
    for (int i = 0; i < key; i++)
    {
        
        if (text.Length%key!=0 && text.Length % key<=i)
        {

                for (int x = 0; x < (Math.Ceiling(text.Length / key)-1); x++)
                {
                Console.Write(tabulka[x][i]);
                }
        }
        else {foreach (var item in tabulka)
        {
            Console.Write(item[i]);
        }}
        
    }
    
    Console.ReadKey();
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