<script>
    import { onMount } from "svelte";
    let canvas;
    let ctx;
    const divider = 25;
    let x_zero_point;
    let y_zero_point;

    onMount(() => {
        ctx = canvas.getContext("2d");
        canvas.width = '500'
        canvas.height = '500'
        x_zero_point = canvas.width / 2;
        y_zero_point = canvas.height / 2
        drawCoordinateSystem()
        drawTriangle()
    })

    function calculateCoordinate(x) {
        return (canvas.width / (canvas.width / divider)) * x;
    }


    function drawCoordinateSystem() {
        ctx.beginPath();
        ctx.moveTo(0, y_zero_point);
        ctx.lineTo(canvas.width, y_zero_point);
        ctx.strokeStyle = "black";
        ctx.stroke();

        ctx.beginPath();
        ctx.moveTo(x_zero_point, 0);
        ctx.lineTo(x_zero_point, canvas.height);
        ctx.stroke();

        for (let i = 0; i <= canvas.width; i += divider) {
            // 수평선
            ctx.beginPath();
            ctx.moveTo(0, i);
            ctx.lineTo(canvas.width, i);
            ctx.strokeStyle = "#e0e0e0";
            ctx.stroke();

            // 수직선
            ctx.beginPath();
            ctx.moveTo(i, 0);
            ctx.lineTo(i, canvas.height);
            ctx.stroke();
        }
    }

    function drawTriangle() {
        ctx.beginPath();

        ctx.moveTo(x_zero_point, y_zero_point);
        ctx.lineTo(x_zero_point + calculateCoordinate(1), y_zero_point);
        ctx.lineTo(x_zero_point, y_zero_point - calculateCoordinate(2));
        ctx.closePath();
        ctx.fillStyle = '#FFCC00';
        ctx.fill();
        ctx.strokeStyle = '#666666';
        ctx.lineWidth = 0;
        ctx.stroke();
    }
</script>

<canvas bind:this={canvas} width="1080" height="1080"></canvas>

<style>
    canvas {
        border: 1px solid #000;
    }
</style>