<script>

    export let current = 0;
    export let progress = 0;
    export let total = 0;

</script>

<aside>

    <div class="current">{current}</div>
    <div class="progress">
        {progress}<span>/</span>{total}
    </div>

</aside>

<style lang="scss">

    aside {
        background-color: blue;
        display: flex;
        justify-content: space-between;
        padding: 0.5rem 1rem;
    }

    .progress {
        span {
            display: inline-block;
            margin: 0 0.1em;
        }
    }

</style>
