<script>


    // @ts-nocheck
    import Prism from 'svelte-prism'
    
    import { Tabs, TabList, TabPanel, Tab } from './tabs.js'
    let sloupce = 0
    let helper = 0;
    let string = 'ahoj';
    let vysledek = 'ahoj';
    let abcd = 'abcdefghijklmnopqrstuvwxyz'
    
    
    
        function handleClick() {
            afinniCipher();
        }
        
        let afinniCipher = () => {
            let decipher = '';
            let array = new Array();
            array.push('mozna');
            array.push('mozna');
            array.push('mozna');
          
            console.log(array[1][0]);
            
           
        
        };
    </script>
    
    <link rel="stylesheet" href="/path/to/styles/default.min.css" />
    <div class="py-8">
        
        <h1 class="text-7xl pb-8 ">Afinní Šifra</h1>
        <p class="text-l pb-8">
            Afinní šifra funguje na principu záměny podobně jako Cézarova šifra. Eliminuje základní nevýhodu
     Cézarovy šifra (málo možností transformace). Pro zašifrování budete potřebovat dva klíče A a B. Klíče 
    musí být celá čísla. Každé písmeno ze zprávy, kterou chcete zašifrovat převedete nejprve na číslo 
    odpovídající pořadí písmena v abecedě následně vynásobíte klíčem A a přičtete k němu klíč B. 
    Výsledek nakonec vydělíte 26(počtem písmen v abecedě). Zbytek po dělení vám dává novou pozici 
    písmena v abecedě po zašifrování.</p>
    <p></p>
    
    <label class="mt-10" for="text">Text k zašifrování</label>	
    <textarea
    class="block p-2.5 shadow appearance-none border rounded w-1/3	 py-2 my-5 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
    name="text"
    bind:value={string}
    />
    

    <button
    class="bg-transparent hover:bg-stone-900 text-stone-900 font-semibold hover:text-white py-2 px-4 border border-stone-900 hover:border-transparent rounded"
    on:click={handleClick}
    >
    Šifrovat
    </button>
    </div>