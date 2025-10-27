<script>
    import { onMount } from "svelte";
    import { fly, slide } from "svelte/transition";

    let toggle = $state(false);

    onMount(function() {
      setTimeout(function() {toggle = true}, 100);  
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

<h1 transition:slide>MENTAL</h1>
{#if toggle}
    <div id="panel" transition:fly={{y:300}}>

    </div>
{/if}