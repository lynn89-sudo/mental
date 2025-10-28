<script>
    import { onMount } from "svelte";
    import { fly, slide } from "svelte/transition";
    import { cubicInOut } from "svelte/easing";

    import { base } from "$app/paths";

    let toggle = $state(false);
    let toggle2 = $state(false);

    onMount(function() {
      setTimeout(function() {toggle = true}, 100);

      if (localStorage.getItem("oneStreak") == null) {
        localStorage.setItem("oneStreak", 0);
        localStorage.setItem("twoStreak", 0);
        localStorage.setItem("threeStreak", 0);
      }
    })
</script>
<style>
    #title {
        font-weight: 900;
        font-size: 80px;
        user-select: none;
        -webkit-user-select: none;
        -moz-user-select: none;
        -ms-user-select: none;
        animation: title 2s infinite;
    }

    .mental {
        -webkit-user-select: none;
        -moz-user-select: none;
        -ms-user-select: none;
    }
    @keyframes title {
        0% {
            transform: translateY(0);
        }
        50% {
            transform: translateY(-10px);
        }
        100% {
            transform: translateY(0);
        }
    }

    #panel {
        position: absolute;
        background-color: rgb(53, 5, 53);
        color: white;
        bottom: 0;
        right: 0;
        left: 0;
        height: 110%;
        border-top-right-radius: 20px;
        border-top-left-radius: 20px;
    }

    table {
        width: 100%;
        text-align: center;
        padding: 20px;

        button {
            font-size: 80px;
            padding: 25px;
            padding-left: 60px;
            padding-right: 60px;
        }
    }
</style>

{#if toggle} 
    <h1 id="title" class="mental" transition:slide={{duration:2000, easing: cubicInOut}}>MENTAL</h1><br><br>
    <h3 class="mental" transition:fly={{ y: 100, delay: 2000 }}>You're mental</h3>
    <h3 class="mental" transition:fly={{ y: 100, delay: 3000 }}>I'm mental</h3>
    <h2 class="mental" style:font-weight={800} transition:fly={{ y: 100, delay: 4500 }}>Math is mental</h2>
{/if}
{#if toggle}
    <div id="panel" transition:fly={{y:1000, delay: 6500}}>
        <br><br><br><br> <br><br><br><br>
        <table>
            <tbody>
                <tr>
                    <td>
                        <button onclick={() => {sessionStorage.setItem("streak", 0); window.location.href = base + "/onedigit";}}>1</button>
                    </td>
                    <td>
                        <button onclick={() => {sessionStorage.setItem("streak", 0); window.location.href = base + "/twodigit";}}>2</button>
                    </td>
                    <td>
                        <button>3</button>
                    </td>
                </tr>
            </tbody>
        </table><br>
        <h1 style:font-weight={900} style:font-size=100px>DIGITS</h1>
        <h3>Choose the mode of mental math you want. All problems are addition or subtraction with the set amount of digits in each number</h3>
    </div>
{/if}