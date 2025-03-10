<!DOCTYPE html>
<html lang="pt">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Predictor Aviator</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: Arial, sans-serif;
        }

        /* Fundo animado com chuva e bolhas */
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background: black;
            color: white;
            text-align: center;
            overflow: hidden;
            position: relative;
        }

        /* Imagem de fundo apenas na tela de login */
        .background-image {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: url('Aviator.jpeg') no-repeat center center fixed;
            background-size: cover;
            opacity: 0.5;
            z-index: 0;
        }

        /* Efeito de chuva e bolhas */
        .rain-container {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            overflow: hidden;
            z-index: -1;
        }

        .rain-drop {
            position: absolute;
            width: 2px;
            height: 15px;
            background: rgba(255, 255, 255, 0.6);
            animation: fall linear infinite;
        }

        @keyframes fall {
            from { transform: translateY(-100vh); }
            to { transform: translateY(100vh); }
        }

        .container {
            background: rgba(34, 34, 34, 0.9);
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0px 0px 10px rgba(255, 255, 255, 0.2);
            width: 300px;
            opacity: 0;
            animation: fadeIn 1s forwards;
            position: relative;
            z-index: 1;
        }

        h2 {
            color: red;
            margin-bottom: 20px;
        }

        .btn {
            width: 100%;
            padding: 10px;
            background-color: red;
            color: white;
            border: none;
            border-radius: 5px;
            font-size: 18px;
            cursor: pointer;
            margin-top: 10px;
        }

        .btn:hover {
            background-color: darkred;
        }

        .prediction-form {
            display: none;
            text-align: center;
        }

        /* Animação de fade-in */
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        /* Círculo animado com efeito colorido */
        .loading-container {
            display: flex;
            justify-content: center;
            align-items: center;
            flex-direction: column;
            margin-top: 20px;
            position: relative;
            width: 175px;
            height: 175px;
            margin: auto;
        }

        .loading-circle {
            width: 175px;
            height: 175px;
            border-radius: 50%;
            border: 10px solid transparent;
            border-top: 10px solid #ff0000;
            border-right: 10px solid #ff7300;
            border-bottom: 10px solid #ffea00;
            border-left: 10px solid #00ff00;
            animation: spin 1s linear infinite, colorChange 3s linear infinite;
            position: absolute;
        }

        /* Animação de rotação */
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        /* Animação de troca de cores */
        @keyframes colorChange {
            0% { border-top-color: #ff0000; }
            25% { border-right-color: #ff7300; }
            50% { border-bottom-color: #ffea00; }
            75% { border-left-color: #00ff00; }
            100% { border-top-color: #ff0000; }
        }

        /* Resultado dentro do círculo (fixo, não gira) */
        .prediction-result {
            position: absolute;
            font-size: 28px;
            font-weight: bold;
            color: yellow;
            display: none;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            z-index: 2;
        }

        .login-form input {
            width: 100%;
            padding: 10px;
            margin: 10px 0;
            border-radius: 5px;
            border: none;
            font-size: 16px;
        }

        /* Botões adicionais */
        .login-form a {
            text-decoration: none;
            width: 100%;
        }
    </style>
</head>
<body>

    <!-- Fundo animado -->
    <div class="background-image login-only"></div>
    <div class="rain-container"></div>

    <!-- Tela de login -->
    <div class="container login-form">
        <h2>PRÉDITOR AVIATOR V8</h2>
        <input type="text" id="username" placeholder="Usuário" required autocomplete="off">
        <input type="password" id="password" placeholder="Senha" required autocomplete="off">
        <button class="btn" onclick="login()">Fazer Login</button>

        <!-- Botão WhatsApp -->
        <a href="https://api.whatsapp.com/send?phone=+258848211454&text=Olá quero comprar robô" target="_blank">
            <button class="btn">Suporte via WhatsApp</button>
        </a>

        <!-- Botão M-Pesa -->
        <a href="https://www.mpesa.com" target="_blank">
            <button class="btn">Pagar via M-Pesa</button>
        </a>
    </div>

    <!-- Tela de previsão -->
    <div class="container prediction-form">
        <h2>Predictor Aviator</h2>

        <!-- Animação do círculo -->
        <div class="loading-container">
            <div class="loading-circle"></div>
            <p class="prediction-result">--.--x</p>
        </div>

        <!-- Botão para prever -->
        <button class="btn" onclick="startCounting()">Prever resultados</button>
    </div>

    <script>
        let patterns = [1.25, 1.80, 1.50, 3.20, 1.10, 2.80, 1.40, 5.00, 1.20, 10.00, 3.02, 1.00, 18, 25, 5.06, 2.00, 1.10, 1.98, 1.45];

        function startCounting() {
            let predictionResult = document.querySelector(".prediction-result");
            let finalValue = patterns[Math.floor(Math.random() * patterns.length)];
            
            let count = 0;
            predictionResult.style.display = "block";

            let interval = setInterval(() => {
                predictionResult.innerText = count.toFixed(2) + "x";
                count += 0.1;

                if (count >= finalValue) {
                    clearInterval(interval);
                    predictionResult.innerText = finalValue.toFixed(2) + "x";
                }
            }, 50);
        }

        function login() {
            document.querySelector('.login-form').style.display = 'none';
            document.querySelector('.prediction-form').style.display = 'block';
            document.querySelector('.background-image').style.display = 'none';
        }

        function createRain() {
            for (let i = 0; i < 100; i++) {
                let drop = document.createElement("div");
                drop.classList.add("rain-drop");
                drop.style.left = Math.random() * 100 + "vw";
                drop.style.animationDuration = Math.random() * 2 + 2 + "s";
                document.querySelector(".rain-container").appendChild(drop);
            }
        }
        createRain();
    </script>

</body>
</html>
