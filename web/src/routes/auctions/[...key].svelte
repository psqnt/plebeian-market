<script context="module">
    export async function load({ params }) {
        const { key } = params
        return { props: { auctionKey: key } }
    }
</script>

<script lang="ts">
    import Auction from "../../lib/components/Auction.svelte"
    import AuctionList from "../../lib/components/AuctionList.svelte";

    export let auctionKey;
</script>

{#if auctionKey === ""}
    <AuctionList />
{:else}
    <Auction auctionKey={auctionKey} />
{/if}