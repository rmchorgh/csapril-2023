<script lang="ts">
    import "../globals.sass";
    import type { Show } from "../app";
    import ShowRow from "../comps/ShowRow.svelte";
    import kuwtc_video from "$lib/kuwtc.mp4";
    import kuwtc_img from "$lib/kuwtc.png";
    import gala0 from "$lib/CSAGala-2.jpg";
    import gala1 from "$lib/CSAGala-3.jpg";
    import gala2 from "$lib/CSAGala-5.jpg";
    import netflix from "$lib/netflix.mp3";
    import logo from "$lib/logo.png";

    import { onMount } from "svelte";
    const gala: string[] = [gala0, gala1, gala2];

    const jouvert: string[] = [
        "https://se-images-blob.campuslabs.com/documents/427/7e9b62e5-82ba-45f6-cce2-08dabb5f3f2a/1500.jpg",
        "https://se-images-blob.campuslabs.com/documents/427/abe1cf69-88d8-4abb-1727-08dab6692024/1500.jpg",
        "https://se-images-blob.campuslabs.com/documents/427/b676260e-18e7-440a-ccdf-08dabb5f3f2a/1500.jpg",
    ];

    const carifest: string[] = [
        "https://se-images-blob.campuslabs.com/documents/427/e721e453-436e-4c57-cce7-08dabb5f3f2a/1500.jpg",
        "https://se-images-blob.campuslabs.com/documents/427/c70dd9b9-59c2-4d74-cce6-08dabb5f3f2a/1500.jpg",
        "https://se-images-blob.campuslabs.com/documents/427/1d699c8b-d7cf-4d7a-cce5-08dabb5f3f2a/1500.jpg",
    ];

    let play = false;
    onMount(() => {
        setTimeout(async () => {
            const e = document.querySelector(".load")!;
            await e
                .querySelector("audio")!
                .play()
                .finally(() => e.remove());
        }, 5050);
    });
</script>

<div class="load">
    <audio src={netflix} type="audio/mp3" autoplay playsinline />
    <div>
        <img src={logo} alt="logo" />
        <h2>RastudoFlix</h2>
    </div>
</div>

<main>
    <section>
        <div class="filter" />
        <video playsinline autoplay loop src={kuwtc_video} />
        <div class="title">
            <img src={kuwtc_img} alt="" />
            <div
                on:click={() => (play = true)}
                class="play {play ? 'button-click' : ''}"
            >
                <p>Play</p>
            </div>
        </div>
    </section>

    <ShowRow
        name="CSA Gala"
        shows={gala.map((thumbnail, i) => ({
            slug: "gala",
            name: `gala-${i}`,
            thumbnail,
            video: "",
        }))}
        date="APR-01"
        ticket={{
            text: "Donate Now",
            href: "google.com",
        }}
    />

    <ShowRow
        name="J'Ouvert"
        shows={jouvert.map((thumbnail, i) => ({
            slug: "jouvert",
            name: `jouvert-${i}`,
            thumbnail,
            video: "",
        }))}
        date="APR-15"
        ticket={{
            text: "Donate Now",
            href: "google.com",
        }}
    />

    <ShowRow
        name="Carifest"
        shows={carifest.map((thumbnail, i) => ({
            slug: "carifest",
            name: `carifest-${i}`,
            thumbnail,
            video: "",
        }))}
        date="APR-23"
        ticket={{
            text: "Get Tickets Now",
            href: "",
        }}
    />
</main>

<style lang="sass">
    $offset: 5%

    .button-click
        animation: click 250ms forwards

    .load
        position: fixed
        top: 0
        width: 100%
        height: 100%
        background: black
        z-index: 1000
        display: flex
        justify-content: center
        align-items: center
        animation: load 5000ms forwards

    section:first-child
        height: 50vh
        position: relative
        display: flex
        align-items: center

    video
        width: calc(100% - $offset)
        margin-left: $offset
        height: 50vh
        object-fit: cover

    .filter
        position: absolute
        width: 100%
        height: 100%
        background: linear-gradient(90deg, rgba(0, 0, 0,1) 0%, rgba(0,0,0,0.45) 30%, rgba(0,0,0,0.15) 100%)

    :global(.row):last-child
        padding-bottom: 8rem

    .title
        position: absolute
        padding: 1em
        img
            width: 30vw

    .play
        display: none
        transform-origin: right center

    @keyframes load
        0%
            opacity: 1
        50%
            opacity: 1
        100%
            opacity: 0
        
    @keyframes click
        50%
            scale: 1.2
        100%
            scale: 1
        
    @media (max-width: 1000px)
        section:first-child
            justify-content: center
            align-items: flex-end
        .play
            display: flex
            flex-direction: row-reverse
            margin-top: 1em
            p
                height: 20px
                color: black
                width: 50px
                padding: 0.5em 1em
                background-color: white
                font-weight: bold
                text-align: center
                border-radius: 0.75em
                margin: 0
        .title
            padding: 1em 0
            img
                width: 80vw

</style>
