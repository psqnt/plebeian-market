<script lang="ts">
    import type { Auction } from "../types/auction";
    import Countdown from "./Countdown.svelte";
    import { ErrorHandler, unfeatureAuction } from "../services/api";
    import { Error, Info, token, user } from "../stores";
    import SvelteMarkdown from 'svelte-markdown';

    function unfeature() {
        unfeatureAuction($token, auction.key,
            () => {
                Info.set("This auction will be prevented from being featured.");
            },
            new ErrorHandler(false, () => Error.set("Failed to unfeature the auction.")));
    }

    export let auction: Auction;
</script>

<div class="my-3 self-center glowbox">
    <div class="card bg-base-300 overflow-hidden shadow-xl my-3">
        <figure class="md:h-max flex justify-center">
            {#each auction.media as photo, i}
                {#if i === 0}
                    <img class="h-full object-fill" src={photo.url} alt="Auctioned object" />
                {/if}
            {/each}
        </figure>
        <div class="card-body">
            <h2 class="justify-center underline card-title mb-2">
                <a href="/auctions/{auction.key}">{auction.title}</a>
            </h2>
            <div class="badge badge-primary self-center md:float-right">{auction.bids.length} bids</div>
            <div class="markdown-container max-h-52 overflow-hidden">
                <SvelteMarkdown source={auction.description} />
            </div>
            <hr class="border-solid border-bg-base-300 divide-y-0 opacity-50 pb-1">
            <Countdown untilDate={auction.end_date} />
            {#if $user && $user.isModerator}
                <div class="btn btn-xs self-center md:float-right" on:click|preventDefault={unfeature}>Unfeature</div>
            {/if}
        </div>
    </div>
</div>