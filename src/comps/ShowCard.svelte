<script lang="ts">
    import type { Show } from "../app.d";
    export let show: Show & {
        date: string;
        ticket?: { href: string; text: string };
    };
    let hovered = false;
    let clicked = false;
</script>

<div
    class="show card {hovered ? 'hovering' : ''} {clicked ? 'active' : ''}"
    on:click={() => {
        clicked = true;
        hovered = false;
    }}
    on:mouseenter={() => {
        hovered = true;
    }}
    on:mouseleave={() => {
        hovered = false;
        clicked = false;
    }}
>
    <img src={show.thumbnail} alt={show.name} />

    <div class="desc {hovered ? 'hovering' : ''} {clicked ? 'active' : ''}">
        <div class="controls">
            <div />
            <div />
            <div />
        </div>
        <h4>100% Match</h4>
        <div class="rating">
            <h5>{show.date}</h5>
            {#if !!show.ticket}
                <a href={show.ticket.href}>{show.ticket.text}</a>
            {/if}
        </div>
    </div>
</div>

<style lang="sass">
.show.card
    background: black
    color: white
    display: flex
    width: 340px
    height: 200px
    flex-direction: column   
    position: relative
    transition: scale 0.5s ease-in-out
    scale: 1
    cursor: pointer
    &.active
        scale: 1.2
        z-index: 10
    &.hovering
        transition-delay: 0.75s
img
    object-fit: cover
    object-position: top

.desc
    padding: 1em
    position: absolute
    opacity: 0
    height: 150px
    transition: opacity 0.125s linear, translate 0.5s ease-in-out
    background-color: black
    width: 100%
    box-sizing: border-box
    z-index: 0
    transform-origin: center center
    &.hovering
        transition-delay: 0.75s
    &.active
        opacity: 1
        translate: 0 190px

.controls
    display: flex
    div
        border-radius: 100%
        border: 2px solid grey
        height: 2em
        width: 2em
        margin-right: 1em
        
.rating
    display: flex
    align-items: center
    h5
        border: 1px solid grey
        padding: 2px 5px
        margin: 0 1em 0 0
        font-size: 0.75em
        color: white
        font-weight: 400
    p
        font-size: 0.85em
        margin: 0
        padding: 0

img
    z-index: 1
    object-fit: cover
    width: 340px
    height: 200px

h4
    color: var(--green)
    margin: 0.5em 0

</style>
