<script>
    export let open = false;
      import { slide } from 'svelte/transition';
      const handleClick = () => open = !open
  </script>
  
            
  <div class="accordion dark:bg-gray-800 rounded-lg text-slate-50 text-center h-12">
    <button class="w-full " on:click={handleClick} >
      <div class="header">
          <div class="text object-center">
              <slot name="head"></slot>	
          </div>
          
          
      </div>
    </button>  
      {#if open}
      <div class="details" transition:slide>
          <slot name="details">
          </slot>
      </div>
      {/if}
  </div>

  
  <style>
      div.accordion {
          margin: 1rem 0;
      }
      
      div.header {
          display:flex;
          width:100%;
      }
      
      div.header .text {
          flex: 1;
          margin-right: 5px;
      }
      
      div.details {
          background-color: white;
          padding:1rem;
      }
  </style>
  