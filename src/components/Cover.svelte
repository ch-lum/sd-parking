<script>
    import { fade } from "svelte-transitions";
</script>

<div in:fade={{ duration: 500 }} out:fade={{ duration: 500 }}>
    <h1>When People Park:<br>San Diego</h1>
    <p>Christopher Lum, Charles Wang, Gino Angelici</p>
    <slot></slot>
</div>

<style>
    div {
        position: absolute;
        top: 0;
        bottom: 0;
        width: 100%;
        height: 100%;
        /* border: 2px solid red; */
        z-index: 2;
        font-family: Georgia;
        text-align: center;
        margin: 0;
    }
    
    h1 {
        padding-top: 5%;
        font-size: 4em;
    }

    p {
        position: absolute;
        top: 0;
        font-family: Helvetica;
        font-size: 1.2em;
    }
</style>