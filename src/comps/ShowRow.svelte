<script lang="ts">
    import type { Show } from "../app";
    import ShowCard from "./ShowCard.svelte";

    export let shows: Show[];
    export let name: string;
    export let date: string;
    export let ticket: { href: string; text: string } | undefined;

    let sectionElement: Element;
    let page = 0;
    let pageLength = 3;

    let hideRight = false;

    const changePage = (dir: number) => {
        page -= dir;
        const cardWidth = 340 + 20;
        const offset = page * pageLength * cardWidth;

        hideRight = Math.abs(page) + 1 >= Math.floor(shows.length / pageLength);

        sectionElement.style.left = offset + "px";
    };
</script>

<div class="row">
    <h2>{name}</h2>
    <section bind:this={sectionElement}>
        {#each shows as show, i}
            <ShowCard show={{ ...show, date, ticket }} />
        {/each}
    </section>
</div>

<style lang="sass">
    $descHeight: 150px
    $picHeight: 200px
    
    $height: $descHeight + $picHeight
    h2
        margin: 0.5em 0 0.5em 1em
        font-weight: 400

    section
        display: flex
        align-items: flex-start
        width: 100vw
        transition: left 0.5s ease-in-out
        position: relative
        height: $picHeight
        padding-bottom: 1em
        & > :global(.show.card)
            margin-right: 20px
            transform-origin: center top
            &:first-child
                margin-left: 1em
                transform-origin: left top
            &:last-child
                margin-right: 1em
                transform-origin: right top
    
    ::-webkit-scrollbar, ::-webkit-scrollbar-button
        width: 1px
        height: 1px
</style>
