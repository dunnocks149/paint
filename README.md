# paint
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Rosie's and Poppy's Colouring Book</title>
    <link href="https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap" rel="stylesheet">
    <script src="https://unpkg.com/@tailwindcss/browser@4"></script>
    <style>
        body {
            font-family: 'Press Start 2P', sans-serif;
            margin: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            background-color: #f0f0f0;
        }

        .container {
            width: 95%;
            max-width: 800px;
            padding: 1.25rem;
            background-color: white;
            border-radius: 0.5rem;
            box-shadow: 0 0.25rem 0.75rem rgba(0, 0, 0, 0.1);
            text-align: center;
        }

        h1 {
            font-size: 1.5rem;
            margin-bottom: 1rem;
            color: #2c3e50;
        }

        #colouringCanvas {
            border: 0.125rem solid #bdc3c7;
            border-radius: 0.25rem;
            margin-bottom: 1rem;
            display: block;
            margin-left: auto;
            margin-right: auto;
            max-width: 100%;
            height: auto;
            max-height: 600px;
        }

        .controls {
            display: flex;
            flex-direction: column;
            align-items: center;
            margin-bottom: 1rem;
        }

        .color-palette {
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
            gap: 0.5rem;
            margin-bottom: 1rem;
        }

        .color-button {
            width: 2rem;
            height: 2rem;
            border-radius: 50%;
            cursor: pointer;
            border: none;
            box-shadow: 0 0.125rem 0.25rem rgba(0, 0, 0, 0.1);
        }

        .color-button.active {
            border: 0.125rem solid #3498db;
            outline: 0.0625rem solid #3498db;
        }

        .shape-palette {
            display: flex;
            justify-content: center;
            gap: 0.5rem;
            margin-bottom: 1rem;
        }

        .shape-button {
            padding: 0.5rem 1rem;
            border-radius: 0.25rem;
            background-color: #ecf0f1;
            color: #2c3e50;
            font-family: 'Press Start 2P', sans-serif;
            cursor: pointer;
            border: none;
            font-size: 0.7rem;
            transition: background-color 0.3s ease;
            box-shadow: 0 0.125rem 0.25rem rgba(0, 0, 0, 0.1);
        }

        .shape-button.active {
            background-color: #3498db;
            color: white;
        }

        .shape-button:hover {
            background-color: #bdc3c7;
        }

        .tool-palette {
            display: flex;
            justify-content: center;
            gap: 0.5rem;
            margin-bottom: 1rem;
        }

        .tool-button {
            padding: 0.5rem 1rem;
            border-radius: 0.25rem;
            background-color: #ecf0f1;
            color: #2c3e50;
            font-family: 'Press Start 2P', sans-serif;
            cursor: pointer;
            border: none;
            font-size: 0.7rem;
            transition: background-color 0.3s ease;
            box-shadow: 0 0.125rem 0.25rem rgba(0, 0, 0, 0.1);
        }

        .tool-button.active {
            background-color: #3498db;
            color: white;
        }

        .tool-button:hover {
            background-color: #bdc3c7;
        }

        #resetButton, #printButton {
            padding: 0.5rem 1rem;
            border-radius: 0.25rem;
            background-color: #3498db;
            color: white;
            font-family: 'Press Start 2P', sans-serif;
            cursor: pointer;
            border: none;
            font-size: 0.7rem;
            transition: background-color 0.3s ease;
            margin: 0.5rem;
        }

        #resetButton:hover, #printButton:hover {
            background-color: #217dbb;
        }

        #printButton {
            background-color: #2ecc71;
        }

        #printButton:hover {
            background-color: #27ae60;
        }

        @media (min-width: 640px) {
            h1 {
                font-size: 2.5rem;
            }
            .controls {
                flex-direction: row;
                justify-content: space-between;
            }
            .color-palette {
                margin-bottom: 0;
            }
            .shape-palette {
                margin-bottom: 0;
            }
            .tool-palette {
                margin-bottom: 0;
            }
        }
    </style>
</head>
<body class="bg-gray-100">
    <div class="container bg-white rounded-lg shadow-md p-4">
        <h1 class="text-2xl font-bold mb-4 text-blue-600">Rosie's and Poppy's Colouring Book</h1>
        <canvas id="colouringCanvas" width="600" height="400"></canvas>
        <div class="controls flex flex-col sm:flex-row items-center sm:justify-between mt-4">
            <div class="color-palette flex flex-wrap justify-center gap-2 mb-4 sm:mb-0">
                <button class="color-button bg-red-500 active" data-color="#ff0000"></button>
                <button class="color-button bg-yellow-500" data-color="#ffff00"></button>
                <button class="color-button bg-blue-500" data-color="#0000ff"></button>
                <button class="color-button bg-green-500" data-color="#00ff00"></button>
                <button class="color-button bg-purple-500" data-color="#800080"></button>
                <button class="color-button bg-orange-500" data-color="#ffa500"></button>
                <button class="color-button bg-pink-500" data-color="#ffc0cb"></button>
                <button class="color-button bg-gray-500" data-color="#808080"></button>
                <button class="color-button bg-black" data-color="#000000"></button>
                <button class="color-button bg-white" data-color="#ffffff"></button>
            </div>
            <div class="shape-palette flex justify-center gap-2 mb-4 sm:mb-0">
                <button class="shape-button active" data-shape="line">Line</button>
                <button class="shape-button" data-shape="circle">Circle</button>
                <button class="shape-button" data-shape="rectangle">Rectangle</button>
            </div>
            <div class="tool-palette flex justify-center gap-2 mb-4 sm:mb-0">
                <button class="tool-button" data-tool="paint">Paint</button>
                <button class="tool-button" data-tool="spray">Spray</button>
                <button class="tool-button" data-tool="fill">Fill</button>
            </div>
            <div class="button-group flex">
                <button id="resetButton" class="bg-blue-500 text-white rounded hover:bg-blue-700 font-['Press_Start_2P'] text-sm mr-2">Reset</button>
                <button id="printButton" class="bg-green-500 text-white rounded hover:bg-green-700 font-['Press_Start_2P'] text-sm">Print</button>
            </div>
        </div>
    </div>

    <script>
        const canvas = document.getElementById('colouringCanvas');
        const ctx = canvas.getContext('2d');
        const colorPalette = document.querySelector('.color-palette');
        const shapePalette = document.querySelector('.shape-palette');
        const toolPalette = document.querySelector('.tool-palette');
        const resetButton = document.getElementById('resetButton');
        const printButton = document.getElementById('printButton');
        const container = document.querySelector('.container');

        let currentColor = '#ff0000';
        let isDrawing = false;
        let lineWidth = 5;
        let currentShape = 'line';
        let currentTool = 'paint';
        let startX, startY;

        // Function to set the active color
        function setActiveColor(color) {
            currentColor = color;
            const colorButtons = document.querySelectorAll('.color-button');
            colorButtons.forEach(button => {
                button.classList.remove('active');
            });
            const activeButton = document.querySelector(`[data-color="${color}"]`);
            if (activeButton) {
                activeButton.classList.add('active');
            }
        }

        // Function to set the active shape
        function setActiveShape(shape) {
            currentShape = shape;
            const shapeButtons = document.querySelectorAll('.shape-button');
            shapeButtons.forEach(button => {
                button.classList.remove('active');
            });
            const activeButton = document.querySelector(`[data-shape="${shape}"]`);
            if (activeButton) {
                activeButton.classList.add('active');
            }
        }

        // Function to set the active tool
        function setActiveTool(tool) {
            currentTool = tool;
            const toolButtons = document.querySelectorAll('.tool-button');
            toolButtons.forEach(button => {
                button.classList.remove('active');
            });
            const activeButton = document.querySelector(`[data-tool="${tool}"]`);
            if (activeButton) {
                activeButton.classList.add('active');
            }
        }

        // Initial drawing setup
        function drawInitialImage() {
            ctx.strokeStyle = 'black';
            ctx.lineWidth = 2;
            ctx.beginPath();

            // Simple house outline
            ctx.moveTo(100, 200);
            ctx.lineTo(200, 100);
            ctx.lineTo(300, 100);
            ctx.lineTo(400, 200);
            ctx.lineTo(400, 300);
            ctx.lineTo(100, 300);
            ctx.lineTo(100, 200);

            // Door
            ctx.moveTo(250, 200);
            ctx.lineTo(250, 300);
            ctx.lineTo(350, 300);
            ctx.lineTo(350, 200);

             // Roof
            ctx.moveTo(200, 100);
            ctx.lineTo(300, 50);
            ctx.lineTo(400, 100);

            ctx.stroke();
        }

        // Set up event listeners
        canvas.addEventListener('mousedown', (e) => {
            isDrawing = true;
            startX = e.offsetX;
            startY = e.offsetY;
            ctx.beginPath();
            ctx.moveTo(startX, startY);
            e.preventDefault();
        });

        canvas.addEventListener('mousemove', (e) => {
            if (isDrawing) {
                ctx.strokeStyle = currentColor;
                ctx.lineWidth = lineWidth;
                if (currentTool === 'paint') {
                    if (currentShape === 'line') {
                        ctx.lineTo(e.offsetX, e.offsetY);
                        ctx.stroke();
                    } else if (currentShape === 'circle') {
                        const radius = Math.sqrt(Math.pow(e.offsetX - startX, 2) + Math.pow(e.offsetY - startY, 2));
                        ctx.clearRect(0, 0, canvas.width, canvas.height);
                        drawInitialImage();
                        ctx.beginPath();
                        ctx.arc(startX, startY, radius, 0, 2 * Math.PI);
                        ctx.stroke();
                    } else if (currentShape === 'rectangle') {
                        const width = e.offsetX - startX;
                        const height = e.offsetY - startY;
                        ctx.clearRect(0, 0, canvas.width, canvas.height);
                        drawInitialImage();
                        ctx.beginPath();
                        ctx.rect(startX, startY, width, height);
                        ctx.stroke();
                    }
                } else if (currentTool === 'spray') {
                    for (let i = 0; i < 10; i++) {
                        const x = e.offsetX + Math.random() * 20 - 10;
                        const y = e.offsetY + Math.random() * 20 - 10;
                        ctx.fillStyle = currentColor;
                        ctx.beginPath();
                        ctx.arc(x, y, 2, 0, 2 * Math.PI);
                        ctx.fill();
                    }
                }
            }
            e.preventDefault();
        });

        canvas.addEventListener('mouseup', () => {
            isDrawing = false;
            ctx.closePath();
        });

        canvas.addEventListener('mouseout', () => {
            isDrawing = false;
            ctx.closePath();
        });

        colorPalette.addEventListener('click', (e) => {
            if (e.target.classList.contains('color-button')) {
                const color = e.target.dataset.color;
                setActiveColor(color);
            }
        });

        shapePalette.addEventListener('click', (e) => {
            if (e.target.classList.contains('shape-button')) {
                const shape = e.target.dataset.shape;
                setActiveShape(shape);
            }
        });

        toolPalette.addEventListener('click', (e) => {
            if (e.target.classList.contains('tool-button')) {
                const tool = e.target.dataset.tool;
                setActiveTool(tool);
            }
        });

        resetButton.addEventListener('click', () => {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            drawInitialImage();
        });

        printButton.addEventListener('click', () => {
            window.print();
        });

        // "Fill" tool functionality
        function fillRegion(x, y, fillColor) {
            const imageData = ctx.getImageData(0, 0, canvas.width, canvas.height);
            const data = imageData.data;

            const startColor = getPixelColor(data, x, y, canvas.width);
            if (colorsMatch(startColor, hexToRgb(fillColor))) {
                return; // Already filled with this color
            }

            const stack = [{ x, y }];
            while (stack.length > 0) {
                const { x, y } = stack.pop();
                if (x < 0 || x >= canvas.width || y < 0 || y >= canvas.height) continue;

                const currentColor = getPixelColor(data, x, y, canvas.width);
                if (!colorsMatch(currentColor, startColor)) continue;

                setPixelColor(data, x, y, canvas.width, hexToRgb(fillColor));

                stack.push({ x: x + 1, y: y });
                stack.push({ x: x - 1, y: y });
                stack.push({ x: x, y: y + 1 });
                stack.push({ x: x, y: y - 1 });
            }
            ctx.putImageData(imageData, 0, 0);
        }

        function getPixelColor(data, x, y, width) {
            const index = (x + y * width) * 4;
            return {
                r: data[index],
                g: data[index + 1],
                b: data[index + 2],
                a: data[index + 3]
            };
        }

        function setPixelColor(data, x, y, width, color) {
            const index = (x + y * width) * 4;
            data[index] = color.r;
            data[index + 1] = color.g;
            data[index + 2] = color.b;
            data[index + 3] = 255; // Full alpha
        }

        function colorsMatch(color1, color2) {
            return color1.r === color2.r && color1.g === color2.g && color1.b === color2.b && color1.a === color2.a;
        }

        function hexToRgb(hex) {
            const bigint = parseInt(hex.slice(1), 16);
            const r = (bigint >> 16) & 255;
            const g = (bigint >> 8) & 255;
            const b = bigint & 255;
            return { r, g, b };
        }

        canvas.addEventListener('click', (e) => {
            if (currentTool === 'fill') {
                fillRegion(e.offsetX, e.offsetY, currentColor);
            }
        });

        // Initialize
        drawInitialImage();
        setActiveColor('#ff0000');
        setActiveShape('line');
        setActiveTool('paint');

    </script>
</body>
</html>
