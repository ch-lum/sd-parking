<script>
    import { fade } from "svelte-transitions";
</script>

<div in:fade={{ duration: 500 }} out:fade={{ duration: 500 }}>
    <h1>Title</h1>
    <slot></slot>
</div>

<style>
    div {
        position: absolute;
        background-color: rgba(177, 6, 6, 0.8);
        top: 0;
        bottom: 0;
        width: 100%;
        height: 100%;
        border: 2px solid red;
        z-index: 2;
        font-family: Georgia;
    }
</style>