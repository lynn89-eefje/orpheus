<script>
    import { onMount } from "svelte";
    import { cubicInOut } from "svelte/easing";
    import { draw, fly, slide } from "svelte/transition";

    let toggle = $state(false);

    onMount(() => {
        setTimeout(() => {toggle = true}, 100);
    })

    let content = $state("");
    let page = $state(0);
    let pagesEnd = 4;
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
        box-shadow: 5px 10px rgb(197, 181, 181), 20px 20px 25px rgba(0, 0, 0, 0.39);

        animation: pulse 3s infinite ease-in-out;
        transition: box-shadow 0.3s ease-in-out;
    }
    #card:hover {
        box-shadow: 8px 13px rgb(167, 152, 152), 30px 30px 25px rgba(0, 0, 0, 0.39);
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
    #page {
        position: absolute;
        transform: translate(-50%, -50%);
        top: 50%;
        left: 50%;
    }
    #page h3 {
        margin-left: 30px;
        margin-right: 30px;
    }
    @media screen and (max-width: 900px) {
        #page.page2 h1 {
            font-size: 30px !important;
        }
        #page.page2 h3 {
            font-size: 10px;
        }
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
            {#if page == 0}
            <div id="page" in:fly={{x:-100, delay:1000}} out:fly={{x:-100}}>
                    <h3>Dear Orpheus,</h3>
                    <svg width="120" height="120" style="margin: 0 auto; display: block;">
                        <path d="M 39.9259 9.4881 C 26.528 9.2542 15.7411 19.8676 15.5107 33.0655 c -0.4712 26.9959 26.6025 34.4695 44.5354 61.3866 c 18.0581 -26.0888 46.3969 -33.7954 46.8506 -59.7915 c 0.2304 -13.198 -10.3795 -24.1848 -23.5775 -24.4152 c -9.5985 -0.1675 -18.095 5.285 -22.0375 13.4174 c -3.6563 -8.2651 -11.7573 -14.0073 -21.3559 -14.1749 z" stroke="darkred" fill="none" stroke-width="10px"/>
                    </svg>
            </div>
            {/if}
            {#if page == 1}
            <div id="page" in:fly={{y:-100, delay:1000}} out:fly={{y:-100}}>
                    <h3>From the moment we first met, on the High Seas...</h3>
                    <img src="images/orph-sea.png" alt="Pirate Orpheus" />
            </div>
            {/if}
            {#if page == 2}
            <div id="page" class="page2">
                    <div style="transform: translateY(-50px)">
                        <h3 in:slide={{delay:1000}} out:slide>you didn't just plunder doubloons,</h3>
                        <h3 in:slide={{delay:2000}} out:slide>you also stole</h3>
                        <h1 in:slide={{delay:2700}} out:slide style="font-size: 50px; font-weight: 900; margin: 0;">MY HEART</h1>
                    </div>
            </div>
            <img in:fly={{delay:3500, y:50}} out:fly={{y:50}} src="images/chest.png" alt="Treasure Chest" style="position: absolute; transform: translate(-50%, -50%); left: 50%; bottom: 40px; max-width: 250px;"/>
            {/if}
            <div id="buttons">
                {#if page > 0}<button onclick={() => {page--}}><span translate = "no" class="material-symbols-outlined">arrow_circle_left</span></button>{/if}{#if page < pagesEnd}<button onclick={() => {page++}}><span translate = "no" class="material-symbols-outlined">arrow_circle_right</span></button>{/if}
            </div>
            <svg width="80" height="80" style="position: fixed; top:30px; left: 20px;">
                <path d="M 15.6931 3.0273 C 13.1911 2.0669 10.4378 3.3237 9.4918 5.7884 c -1.9352 5.0413 2.6418 8.2979 4.1708 14.5833 c 5.1784 -3.6678 11.0315 -3.1777 12.895 -8.0323 c 0.9461 -2.4647 -0.2964 -5.2553 -2.761 -6.2014 c -1.7925 -0.6881 -3.7623 -0.2445 -5.0595 1.0142 c -0.1218 -1.8034 -1.2515 -3.4368 -3.044 -4.1248 z" stroke="black" fill="black"/>
            </svg>
            <svg width="110" height="110" style="position: fixed; bottom: 200px; right: 5px;">
                <path d="M 62.4689 11.0223 C 59.0884 11.8651 57.0936 15.2564 57.9238 18.5865 c 1.6983 6.8115 9.0005 6.8665 15.3155 12.4198 c 2.7795 -7.7671 9.378 -11.6096 7.7426 -18.1688 c -0.8303 -3.3301 -4.2342 -5.3753 -7.5642 -4.5451 c -2.4219 0.6038 -4.1887 2.5449 -4.6316 4.8526 c -1.4744 -1.8297 -3.8953 -2.7266 -6.3172 -2.1228 z" fill="black"/>
            </svg>
            <h2 style="user-select: none; -webkit-user-select: none; position:fixed; right: 40px; bottom: 30px; transform: rotate(-5deg)">^w^</h2>
            <h2 style="user-select: none; -webkit-user-select: none; position:fixed; right: 40px; top: 30px; transform: rotate(8deg)">:3</h2>
            <h2 style="user-select: none; -webkit-user-select: none; position:fixed; left: 40px; top: 90px; transform: rotate(-5deg)">{">~<"}</h2>
            <h2 style="user-select: none; -webkit-user-select: none; position:fixed; right: 30px; bottom:180px; transform: rotate(-5deg)"><span class="material-symbols-outlined">kid_star</span></h2>

            <h2 style="user-select: none; -webkit-user-select: none; position:fixed; left: 40px; bottom:180px; transform: rotate(-5deg)"><span class="material-symbols-outlined">kid_star</span></h2>
            <h2 style="user-select: none; -webkit-user-select: none; position:fixed; right: 20px; top:170px; transform: rotate(9deg);"><span class="material-symbols-outlined" style:font-size="60px;">kid_star</span></h2>

            <svg width="80" height="80" style="position: fixed; bottom:90px; right: 10px;">
                <path d="M 15.6931 3.0273 C 13.1911 2.0669 10.4378 3.3237 9.4918 5.7884 c -1.9352 5.0413 2.6418 8.2979 4.1708 14.5833 c 5.1784 -3.6678 11.0315 -3.1777 12.895 -8.0323 c 0.9461 -2.4647 -0.2964 -5.2553 -2.761 -6.2014 c -1.7925 -0.6881 -3.7623 -0.2445 -5.0595 1.0142 c -0.1218 -1.8034 -1.2515 -3.4368 -3.044 -4.1248 z" stroke="black" fill="black"/>
            </svg>
            <h2 style="user-select: none; -webkit-user-select: none; position:fixed; left: 40px; bottom: 40px; transform: rotate(8deg)">:P</h2>
            <h2 style="user-select: none; -webkit-user-select: none; position:fixed; left: 30px; top: 130px; transform: rotate(8deg)">hehe</h2>
            <h2 style="user-select: none; -webkit-user-select: none; position:fixed; right: 30px; top: 70px; transform: rotate(-8deg)">orphy!</h2>

            <h2 style="user-select: none; -webkit-user-select: none; position:fixed; left: 20px; top:200px; transform: rotate(9deg);"><span class="material-symbols-outlined" style:font-size="50px;">filter_vintage</span></h2>
            <svg width="110" height="110" style="position: fixed; bottom: 40px; left: 5px;">
                <path d="M 62.4689 11.0223 C 59.0884 11.8651 57.0936 15.2564 57.9238 18.5865 c 1.6983 6.8115 9.0005 6.8665 15.3155 12.4198 c 2.7795 -7.7671 9.378 -11.6096 7.7426 -18.1688 c -0.8303 -3.3301 -4.2342 -5.3753 -7.5642 -4.5451 c -2.4219 0.6038 -4.1887 2.5449 -4.6316 4.8526 c -1.4744 -1.8297 -3.8953 -2.7266 -6.3172 -2.1228 z" fill="black"/>
            </svg>
        </div>
    </div>
{/if}