# calculadora-basica
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculadora Básica</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }

        .calculadora {
            background-color: #333;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 15px rgba(0, 0, 0, 0.3);
            width: 300px;
        }

        .pantalla {
            background-color: #222;
            color: white;
            font-size: 2rem;
            padding: 10px;
            text-align: right;
            border: none;
            border-radius: 5px;
            margin-bottom: 15px;
            width: 100%;
            box-sizing: border-box;
        }

        .botones {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 10px;
        }

        button {
            padding: 15px;
            font-size: 1.2rem;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            background-color: #555;
            color: white;
            transition: background-color 0.2s;
        }

        button:hover {
            background-color: #777;
        }

        .operador {
            background-color: #ff9500;
        }

        .operador:hover {
            background-color: #ffb143;
        }

        .igual {
            background-color: #4caf50;
        }

        .igual:hover {
            background-color: #6fcf74;
        }

        .limpiar {
            background-color: #f44336;
        }

        .limpiar:hover {
            background-color: #ff6659;
        }
    </style>
</head>
<body>
    <div class="calculadora">
        <input type="text" class="pantalla" id="pantalla" disabled>

        <div class="botones">
            <button class="limpiar" onclick="limpiar()">C</button>
            <button onclick="borrarUltimo()">⌫</button>
            <button class="operador" onclick="agregarOperador('/')">/</button>
            <button class="operador" onclick="agregarOperador('*')">×</button>

            <button onclick="agregarNumero('7')">7</button>
            <button onclick="agregarNumero('8')">8</button>
            <button onclick="agregarNumero('9')">9</button>
            <button class="operador" onclick="agregarOperador('-')">-</button>

            <button onclick="agregarNumero('4')">4</button>
            <button onclick="agregarNumero('5')">5</button>
            <button onclick="agregarNumero('6')">6</button>
            <button class="operador" onclick="agregarOperador('+')">+</button>

            <button onclick="agregarNumero('1')">1</button>
            <button onclick="agregarNumero('2')">2</button>
            <button onclick="agregarNumero('3')">3</button>
            <button class="igual" onclick="calcular()">=</button>

            <button onclick="agregarNumero('0')" style="grid-column: span 2;">0</button>
            <button onclick="agregarNumero('.')">.</button>
        </div>
    </div>

    <script>
        let pantalla = document.getElementById('pantalla');

        function agregarNumero(num) {
            pantalla.value += num;
        }

        function agregarOperador(op) {
            // Evitar operadores consecutivos
            let ultimoCaracter = pantalla.value.slice(-1);
            if (['+', '-', '*', '/'].includes(ultimoCaracter)) {
                pantalla.value = pantalla.value.slice(0, -1) + op;
            } else {
                pantalla.value += op;
            }
        }

        function limpiar() {
            pantalla.value = '';
        }

        function borrarUltimo() {
            pantalla.value = pantalla.value.slice(0, -1);
        }

        function calcular() {
            try {
                // Evaluar la expresión (¡cuidado en producción!)
                pantalla.value = eval(pantalla.value).toString();
            } catch (e) {
                pantalla.value = 'Error';
                setTimeout(limpiar, 1500);
            }
        }
    </script>
</body>
</html>
