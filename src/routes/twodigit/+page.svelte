<script>
    import { base } from "$app/paths";

    import { onMount } from "svelte";
    import { preventDefault } from "svelte/legacy";
    import { fly, slide } from "svelte/transition";

    let toggle = $state(false);

    let sign = $state("+");
    let signNum = ((Math.random() * 10) + 1);
    let factor = $state(1);
    signNum = Math.floor(signNum);
    //console.log(signNum);
    if (signNum%2 == 0) {
        sign = "-";
        factor = -1;
    }
    let n1 = $state(0);
    let n2 = $state(0);

    let num = ((Math.random() * 99) + 1);
    num = Math.floor(num);
    n1 = num;
    num = ((Math.random() * 99) + 1);
    num = Math.floor(num);
    n2 = num;

    let feedback = $state(false);
    let result = $derived(n1+n2*factor);
    let answer = $state();
    let wrong = $state(true);

    function submitAns() {
        if (result == answer && wrong) {
            wrong = false;
            feedback = false;
            sessionStorage.setItem("streak", parseInt(sessionStorage.getItem("streak")) + 1)
            window.location.href = base + "/twodigit";
        }
        else {
            feedback = true;
            wrong = true;
            // window.location.href = base + "/fail";
        }
    }

    let countdown = $state(9);

    onMount(function() {
      setTimeout(function() {toggle = true}, 100);  
      sessionStorage.setItem("mode", "two");
    })

    onMount(function() {
        setInterval(function() {
            if (wrong) {
                countdown--;
            }
            if (countdown <= 0) {
                window.location.href = base + "/fail";
                countdown = 0;
            }
        }, 1000);
    })
</script>
<style>
    h1 {
        font-weight: 900;
        font-size: 80px;
        user-select: none;
        -webkit-user-select: none;
        -moz-user-select: none;
        -ms-user-select: none;
    }

    #panel {
        position: absolute;
        background-color: rgb(53, 5, 53);
        color: white;
        bottom: 0;
        right: 0;
        left: 0;
        height: 65%;
        border-top-right-radius: 20px;
        border-top-left-radius: 20px;
    }

    form {
        text-align: center;
        font-size: 60px;
        input {
            width: 200px;
            font-family: Montserrat;
            font-weight: 900;
            text-align: center;
        }
    }
</style>

<h1 transition:slide>TWO DIGIT</h1>
<h3>Complete each question within 8 seconds</h3>
<br>
<h2>{countdown} seconds remain</h2>
<br>
<h2><button onclick={() => {window.location.href = base}}>Exit and Terminate Round</button></h2>
{#if toggle}
    <div id="panel" transition:fly={{y:300}}>
        <br><br><br>
        <h1><span style:opacity={0} style:font-weight=600px>{sign}</span> {n1}</h1>
        <h1>{sign} {n2}</h1>
        <h3>___________</h3>
        <br>
        <form id="answer" onsubmit={() => {event.preventDefault(); submitAns();}}>
            <input type="number" bind:value={answer} placeholder=0 max=198 min=-198/><br>
            <button type="submit" onclick={submitAns}>Submit</button>
        </form>
        <br>
        {#if feedback}
            <h3>Wrong answer, try again!</h3>
        {/if}
    </div>
{/if}