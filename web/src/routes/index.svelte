<svelte:head>
    <title>Plebeian Market</title>
</svelte:head>

<script lang="ts">
    import PublicAuctionCard from "../lib/components/PublicAuctionCard.svelte";
    import Typewriter from "../lib/components/Typewriter.svelte";
    import type { Auction } from "../lib/types/auction";
    import { getFeaturedAuctions } from "../lib/services/api";
    import { onMount } from "svelte";

    let auctions: Auction[] | null = null;

    onMount(async () => {
        getFeaturedAuctions(a => { auctions = a; });
    });
</script>

<div class="md:hidden">
    <Typewriter />
</div>
<div class="flex justify-center">
    <div class="md:flex justify-center mt-0 md:mt-14 md:columns-3 w-3/5">
        <div class="flex items-center mt-1">
            <div class="text-7xl ml-9 md:ml-0 md:text-9xl">1</div>
            <div class="flex flex-col">
                <div><img class="max-h-24 ml-4 md:ml-0 md:max-h-48" src="/images/bitko_01.png" alt="Tweet!"></div>
                <div class="-translate-y-1 md:-translate-y-0 h-full ml-2 text-xl">Tweet Photos</div>
            </div>
        </div>
        <div class="flex -translate-y-3 md:-translate-y-0 items-center mt-1">
            <div class="text-7xl ml-9 md:ml-0 md:text-9xl">2</div>
            <div class="flex flex-col">
                <div><img class="max-h-24 ml-4 md:ml-0 md:max-h-48" src="/images/bitko_02.png" alt="Start!"></div>
                <div class="-translate-y-1 md:-translate-y-0 h-full ml-2 text-xl">Click Start</div>
            </div>
        </div>
        <div class="flex -translate-y-3 md:-translate-y-0 items-center mt-1">
            <div class="text-7xl ml-9 md:ml-0 md:text-9xl">3</div>
            <div class="flex flex-col">
                <div><img class="max-h-24 ml-4 md:ml-0 md:max-h-48" src="/images/bitko_03.png" alt="Stack!"></div>
                <div class="-translate-y-1 md:-translate-y-0 h-full ml-2 text-xl">Stack Sats</div>
            </div>
        </div>
    </div>
</div>
<div class="hidden md:flex-container md:ml-20 md:flex md:justify-center md:justify-items-start mt-12 px-8 columns-1 gap-0 md:columns-3 md:w-11/12">
    <Typewriter />
</div>
<div class="md:pt-10 mb-0 md:mb-4 -translate-y-3 md:-translate-y-0 text-2xl flex justify-center">
    Let's get the market started...
</div>
<div class="flex justify-center items-center">
    <div class="glowbutton glowbutton-go mb-5" on:click={() => { window.location.href = `${window.location.protocol}//${window.location.host}/login`; }}></div>
</div>
<div class="grid lg:grid-cols-3 gap-4">
    {#if auctions !== null}
        {#each auctions as auction}
            <div class="h-auto">
                <PublicAuctionCard auction={auction} />
            </div>
        {/each}
    {/if}
</div>
