<script>
    export let text = "";
</script>

<div class="tooltip" style="display: {text ? 'block' : 'none'}">
    {text}
</div>

<style>
    .tooltip {
        position: absolute;
        padding: 10px;
        background: blue;
        border: 1px solid black;
        border-radius: 5px;
        pointer-events: none;
    }
</style>