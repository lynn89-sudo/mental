<script>
    import { onMount } from "svelte";
    import { fly, slide } from "svelte/transition";

    import { base } from "$app/paths";

    let toggle = $state(false);
    let toggle2 = $state(false);

    onMount(function() {
      setTimeout(function() {toggle = true}, 100);
      setTimeout(function() {toggle2 = true}, 3000); 
      setTimeout(function() {window.location.href= path + "/onedigit"}) 
    })
</script>
<style>
    h1 {
        font-weight: 900;
        font-size: 80px;
        animation: flash 2s infinite;
        user-select: none;
        -webkit-user-select: none;
        -moz-user-select: none;
        -ms-user-select: none;
    }
    .mental {
        -webkit-user-select: none;
        -moz-user-select: none;
        -ms-user-select: none;
    }
    @keyframes flash {
        0% {
            color: black;
        }
        50% {
            color: purple;
        }
        100% {
            color: black;
        }
    }

    #panel {
        position: absolute;
        background-color: rgb(53, 5, 53);
        color: white;
        bottom: 0;
        right: 0;
        left: 0;
        height: 75%;
        border-top-right-radius: 20px;
        border-top-left-radius: 20px;
    }
</style>

{#if toggle} 
    <h1 transition:slide>MENTAL</h1>
    <h3 class="mental" transition:fly={{ y: 100, delay: 1000 }}>You're mental</h3>
    <h3 class="mental" transition:fly={{ y: 100, delay: 1500 }}>I'm mental</h3>
    <h2 class="mental" style:font-weight={800} transition:fly={{ y: 100, delay: 2000 }}>Math's mental</h2>
{/if}
{#if toggle2}
    <div id="panel" transition:fly={{y:300}}>

    </div>
{/if}