<script>

    import p5 from 'p5';

    let id;

    let capture;
    let grid = {
        columns: 3,
        rows: 3,
        w: 0,
        h: 0
    };

    const s = ( sketch ) => {
        sketch.setup = () => {
            sketch.createCanvas(container.offsetWidth, container.offsetHeight);
            sketch.frameRate( 3 );

            capture = sketch.createCapture(sketch.VIDEO);
            // capture.hide();
            capture.size( grid.columns, grid.rows );

            grid.w = ( sketch.width / grid.columns ) + 1;
            grid.h = ( sketch.height / grid.rows ) + 1;

            sketch.fill( 255, 0, 0 );
            sketch.noStroke();

        };
        sketch.draw = () => {

            let pixels = [];

            for ( let y = 0; y < grid.rows; y++ ) {
                for ( let x = 0; x < grid.columns; x++ ) {

                    let p = capture.get( x, y );
                    let c = Math.round( ( (p[0] + p[1] + p[2]) / 765 ) * 1.2 );

                    pixels.push( c );

                    sketch.fill( c * 255 );
                    sketch.rect( grid.w * x, grid.h * y, grid.w + 1, grid.h + 1 );

                }
            }

            id = pixels;

        };
    };

    let container;
    let myp5;

    import { onMount } from 'svelte';
    onMount(()=>{
        myp5 = new p5(s, container);
    });

</script>

<div bind:this={container}></div>

<style lang="scss">

    div {
        width: 100%;
        height: 100%;
    }

    :global( video ){
        opacity: 0;
        display: absolute;
        top: 0;
    }

</style>
