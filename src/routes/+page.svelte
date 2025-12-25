<script>
    import { onMount } from "svelte";
    import { cubicInOut } from "svelte/easing";
    import { fly } from "svelte/transition";

    let toggle = $state(false);

    onMount(() => {
        setTimeout(() => {toggle = true}, 100);
    })

    let content = $state("");
    let page = $state(0);
    let pages = ["a", "b", "c"];
</script>
<style>
    #card {
        position: fixed;
        background-color: aliceblue;
        top: 45px;
        bottom: 55px;
        right: 70px;
        left: 70px;
        transform: rotate(0.5deg);
        border-radius: 20px;
        box-shadow: 5px 10px rgb(197, 181, 181);

        animation: pulse 3s infinite ease-in-out;
        transition: box-shadow 0.3s ease-in-out;
    }
    #card:hover {
        box-shadow: 10px 15px rgb(167, 152, 152);
    }
    @keyframes pulse {
        0% {
            transform: rotate(0.5deg);
            
        }
        50% {
            transform: rotate(1.5deg);
        }
        100% {
            transform: rotate(0.5deg);
        }
    }

    #content {
        position: relative;
        width: 100%;
        height: 100%;
    }

    #buttons {
        position: absolute;
        bottom: 30px;
        transform: translate(-50%, 0%);
        left: 50%;
    }
</style>
{#if toggle}
    <div id="card" transition:fly={{y:-200, easing: cubicInOut, duration:1200}}>
        <div id="content">
            {@html content}
            <div id="buttons">
                {#if page > 0}<button onclick={() => {page--}}><span class="material-symbols-outlined">arrow_circle_left</span></button>{/if}{#if page < pages.length-1}<button onclick={() => {page++}}><span class="material-symbols-outlined">arrow_circle_right</span></button>{/if}
            </div>
        </div>
    </div>
{/if}