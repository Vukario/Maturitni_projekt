<script>
    // @ts-nocheck
    import Prism from 'svelte-prism'
    
    
    export let highlight = 0;
    export let kroky;
    
    let pocetKroku = 0;
   
    export let postup;
    export let cats;
    
   
    function handleClick2() {
        
		
        console.log(kroky[highlight])
        highlight+=1;
        pocetKroku+=1;
        const el = document.querySelector("#line"+kroky[highlight]);
        console.log("line"+kroky[highlight]);
        console.log(el);
        el.scrollIntoView({
            behavior: 'smooth',
            top: 20
        });
	}
    </script>
    
    
    <div class="w-3/4">
    {#if highlight>0}
        
    

     <Prism></Prism>
     
     
    {#each cats as cat, i}
    {#if cat.id == kroky[highlight]}    
    <div id="line{cat.id}">
	<pre><code class="javascript"><div class="bang">{cat.name}</div></code></pre>
    </div>
    {:else}
    <div id="line{cat.id}">
	<Prism  language="javascript">
    {cat.name}
    </Prism>
    </div>
    {/if}
    {/each}
    
    <Prism></Prism>
    
    <h2 class="text-7xl pb-8 text-red-900">{postup[highlight]}</h2>
                            {/if}
    </div>
    {#if pocetKroku!=kroky.length-1}
    <button
    class="fixediv bg-transparent w-30 hover:bg-stone-900  text-stone-900 font-semibold hover:text-white py-2 px-4 border border-stone-900 hover:border-transparent rounded"
    on:click={handleClick2}
    >
    Pokračovat
    </button>
    {:else}
    <button
    class="fixediv bg-transparent w-30 hover:bg-stone-900  text-stone-900 font-semibold hover:text-white py-2 px-4 border border-stone-900 hover:border-transparent rounded"
    
    >krokování dokončeno</button>
    {/if}
   
    
    
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
        .fixediv {
    position: fixed;
    bottom: 50%;
    right: 2%;

    }
    </style>