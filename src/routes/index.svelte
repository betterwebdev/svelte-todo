
<script>
    import { slide } from "svelte/transition";
import { elasticInOut } from "svelte/easing";

    let text = ''
    let i = [
        
    ]

    function Add(){
        if (text){
            i=[
                ...i,{
                    item: text,
                    checked: false,
                    id: Math.random().toString(36)
                }
            ]
        }
        text=''
    }

    function Remove(id){
        const index = i.findIndex(a => a.id === id);
  i.splice(index, 1);
  i = i;
    }
</script>
<h1 class="p-4 text-center font-medium font-sans text-3xl max-w mt-6">My First Svelte App (With Tailwind)</h1>
<div class="flex flex-col items-center content-center text-center space-y-3">
{#each i as x, index}
<div  class=" flex  px-10 flex-row items-center content-center space-x-10 " transition:slide="{{duration: 300, easing: elasticInOut}}">

<h1>{x.item}</h1>
<button class="bg-red-400 rounded-md text-white p-2 m-2 px-6" on:click={()=> Remove(x.id)}>Delete</button>
</div>
{/each}
</div>
<div class="flex content-center items-center mx-auto">
<form class="mt-5 mx-auto content-center items-center"   on:submit|preventDefault="{Add}">
    <input bind:value={text} class="border-2 border-gray-300 rounded-md bg-white focus:outline-none p-4 py-3 mb-2 mr-0" placeholder="Type item here">
<button class="bg-blue-500 font-medium font-sans  rounded-md text-white mx-auto m-4 p-3 px-8 ml-2" type="submit">Add Item</button>
</form>
</div>