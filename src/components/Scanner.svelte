<script>

    let video, canvas, context;

    let width = 64;
    let height = 64;
    let resolution = 10;
    let frameRate = 10;

    import { onMount } from 'svelte';
    onMount(()=>{

        navigator.mediaDevices.getUserMedia({
            video: {
                width:     width,
                height:    height,
                frameRate: frameRate
            }
        }).then(function(stream) {
            video.srcObject = stream;
            video.onloadedmetadata = function(e) {
                video.play();
            };
        }).catch(function(err) {
            // deal with an error (such as no webcam)
        });

        canvas.width = width * resolution;
        canvas.height = height * resolution;

        context = canvas.getContext('2d');
        context.drawImage(video, 0, 0, canvas.width, canvas.height);
        context.mozImageSmoothingEnabled = false;
        context.imageSmoothingEnabled = false;

        // video 'play' event listener
        video.addEventListener('play', function() {
            tick();
        }, false);

    });

    function tick() {
        pixel();
        pixel2();
        setTimeout(tick, Math.round(1000/frameRate));
    }

    let threshold = ( 255 * 3 ) * 0.5;

    function pixel() {

        let w = canvas.width / resolution;
        let h = canvas.height / resolution;
        context.drawImage(video, 0, 0, w, h);

        let image = context.getImageData(0, 0, w, h);
        let data = image.data;

        for( let i = 0; i < data.length; i = i+4 ){
            let brightness = data[i] + data[i+1] + data[i+2];
            data[i] = data[i+1] = data[i+2] = brightness < threshold ? 0 : 255;
        }

        image.data.set(data);
        context.putImageData(image, 0, 0);
        context.drawImage(canvas, 0, 0, w, h, 0, 0, width * resolution, height * resolution);
    }

    let code = '';

    function pixel2() {

        code = [];

        let w = 2;
        let h = 2;
        context.drawImage(video, 0, 0, w, h);

        let image = context.getImageData(0, 0, w, h);
        let data = image.data;

        for( let i = 0; i < data.length; i = i+4 ){
            code.push( ( data[i] + data[i+1] + data[i+2] ) < threshold ? 1 : 0 );
        }

        code = parseInt( code.join(''), 2);
    }

</script>

{code}

<video bind:this={video} autoplay></video>
<canvas bind:this={canvas}></canvas>

<style lang="scss">

    video, canvas {
        border: 1px solid #333;
        margin: 1rem;
    }

</style>
