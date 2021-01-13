<script>

    import Scanner from './components/Scanner.svelte';
    import Display from './components/Display.svelte';
    import Info from './components/Info.svelte';

</script>

<div class="wrapper">

    <main>

        <Scanner />
        <!-- <Display /> -->

    </main>

    <Info/>

</div>

<style lang="scss">

    .wrapper {
        position: fixed;
        top: 0;
        left: 0;
        width: 100vw;
        height: 100vh;
        display: flex;
        flex-direction: column;
    }

    main {
        flex: 1;
        position: relative;
    }

</style>
