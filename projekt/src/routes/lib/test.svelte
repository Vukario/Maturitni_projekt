<script>
    // @ts-nocheck
    import Prism from 'svelte-prism'
    
    
    export let highlight = 0;
    export let kroky;
   
    export let postup;
    let cats = [
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
    function handleClick2() {
        
		
        console.log(kroky[highlight])
        highlight+=1;
	}
    </script>
    
    {#if highlight>0}
        
    
     
     <Prism></Prism>
     
     
    {#each cats as cat, i}
    {#if cat.id == kroky[highlight]}
	<pre><code class="javascript"><div class="bg-black bang">{cat.name}</div></code></pre>
    {:else}
	<Prism language="javascript">
    {cat.name}
    </Prism>
    {/if}
    {/each}
    
    <Prism></Prism>
    
    <h2 class="text-7xl pb-8 text-red-900">{postup[highlight]}</h2>
                            {/if}
               
   
    <button
   
    class="bg-transparent w-full hover:bg-stone-900 text-stone-900 font-semibold hover:text-white py-2 px-4 border border-stone-900 hover:border-transparent rounded"
    on:click={handleClick2}
    >
    Krokovat
    </button>
    
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
        .bang {
           background-color:  rgb(31,41,55);
           color: white;
        }
    </style>