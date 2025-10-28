<script>
    import { base } from "$app/paths";
    import { onMount } from "svelte";

    let streak = $state(0);
    let highestStreak = $state(0);
    let trial = $state("");
    let congrats = $state(false);
    let typeLabel = $state("One");

    onMount(function() {
        if (sessionStorage.getItem("mode") == null) {
            window.location.href = base;
        }
        trial = sessionStorage.getItem("mode");
        streak = sessionStorage.getItem("streak");
        
        if (trial === "one") {
            highestStreak = localStorage.getItem("oneStreak");
            if (streak > highestStreak) {
                highestStreak = streak;
                localStorage.setItem("oneStreak", highestStreak)
                congrats = true;
            }
        }
        if (trial === "two") {
            typeLabel = "Two";
            highestStreak = localStorage.getItem("twoStreak");
            if (streak > highestStreak) {
                highestStreak = streak;
                localStorage.setItem("twoStreak", highestStreak)
                congrats = true;
            }
        }
        if (trial === "three") {
            typeLabel = "Three";
            highestStreak = localStorage.getItem("threeStreak");
            if (streak > highestStreak) {
                highestStreak = streak;
                localStorage.setItem("threeStreak", highestStreak)
                congrats = true;
            }
        }
        sessionStorage.removeItem("streak");
        sessionStorage.removeItem("mode")
    })
</script>
<svelte:head>
    <title>Mental - End of Round</title>
</svelte:head>
<style>
    h1 {
        font-weight: 900;
    }
</style>
<br><br>
<h1>UH OH</h1>
<h3>You ran out of time</h3>
<br>
<h2>:(</h2>
<br>
<h2><button onclick={() => {window.location.href = base}}>Return</button></h2>
<br>
<br>
<h1 style:font-size=70px>{streak} problems solved</h1>
<h3>{typeLabel}-digit mode</h3><br>
<h3>------------------------------------------</h3>
<br>
<h3>Highest Streak for {typeLabel}-Digit mode</h3>
<h1 style:font-size=70px>{highestStreak} problems</h1>
<br>
{#if congrats}
    <h2>Great job beating your streak!</h2>
{:else}
    <h2>Better luck next time</h2>
{/if}

