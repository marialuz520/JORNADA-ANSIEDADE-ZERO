<!DOCTYPE html>
<html lang="pt">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Controle Sua Ansiedade</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            padding: 20px;
        }
        .container {
            max-width: 500px;
            margin: auto;
            padding: 20px;
            border: 1px solid #ccc;
            border-radius: 10px;
            box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.1);
        }
        button {
            background-color: #4CAF50;
            color: white;
            border: none;
            padding: 10px 20px;
            cursor: pointer;
            border-radius: 5px;
            margin: 5px;
        }
        button:hover {
            background-color: #45a049;
        }
        .exercise, .extra-questions, .timer, .chatbot {
            margin-top: 20px;
            display: none;
        }
        .hidden { display: none; }
    </style>
</head>
<body>
    <div class="container">
        <h1>Como está seu humor hoje?</h1>
        <p>Escolha um emoji para descrever como se sente agora:</p>
        <button onclick="selectMood('😀')">😀 Feliz</button>
        <button onclick="selectMood('😐')">😐 Neutro</button>
        <button onclick="selectMood('😟')">😟 Ansioso</button>
        <button onclick="selectMood('😢')">😢 Triste</button>
        
        <div id="advice" style="margin-top:20px; display:none;"></div>
        <div id="exercise" class="exercise"></div>
        <div id="extra-questions" class="extra-questions"></div>
        <div id="timer" class="timer"></div>
        <div id="chatbot" class="chatbot"></div>
    </div>
    
    <script>
        function selectMood(mood) {
            let adviceText = "";
            let exerciseText = "";
            let questionsHtml = "";
            if (mood === "😀") {
                adviceText = "Ótimo! Continue praticando gratidão e aproveite seu dia!";
                exerciseText = "Exercício: Escreva 3 coisas pelas quais você é grato hoje.";
                questionsHtml = "Qual foi o melhor momento do seu dia até agora?";
            } else if (mood === "😐") {
                adviceText = "Que tal um exercício de respiração para melhorar o foco?";
                exerciseText = "Exercício: Feche os olhos e respire fundo por 4 segundos, segure por 4 segundos e solte por 4 segundos. Repita 5 vezes.";
                questionsHtml = "O que você pode fazer agora para melhorar seu dia?";
            } else if (mood === "😟") {
                adviceText = "Respire fundo por 4 segundos, segure por 4 segundos e solte por 4 segundos.";
                exerciseText = "Exercício: Experimente a técnica de ancoragem - toque em um objeto próximo e concentre-se em sua textura para se conectar ao presente.";
                questionsHtml = "Existe algo que você pode mudar agora para se sentir melhor?";
            } else {
                adviceText = "Ouça uma música relaxante e tente um exercício de relaxamento.";
                exerciseText = "Exercício: Alongue os braços e pernas lentamente, prestando atenção à sensação do seu corpo.";
                questionsHtml = "O que você pode fazer agora para se sentir um pouco mais leve?";
            }
            
            document.getElementById('advice').innerHTML = `<h3>Sugestão para você:</h3><p>${adviceText}</p>`;
            document.getElementById('advice').style.display = 'block';
            document.getElementById('exercise').innerHTML = `<h3>Pratique este exercício:</h3><p>${exerciseText}</p>`;
            document.getElementById('exercise').style.display = 'block';
            document.getElementById('extra-questions').innerHTML = `<h3>Reflexão:</h3><p>${questionsHtml}</p>`;
            document.getElementById('extra-questions').style.display = 'block';
            
            startTimer();
            startChatbot();
        }
        
        function startTimer() {
            let timerDiv = document.getElementById('timer');
            timerDiv.innerHTML = "<h3>Relaxamento em andamento...</h3><p>5:00</p>";
            timerDiv.style.display = 'block';
            let time = 300;
            let countdown = setInterval(() => {
                let minutes = Math.floor(time / 60);
                let seconds = time % 60;
                timerDiv.innerHTML = `<h3>Relaxamento em andamento...</h3><p>${minutes}:${seconds < 10 ? '0' : ''}${seconds}</p>`;
                if (time === 0) {
                    clearInterval(countdown);
                    timerDiv.innerHTML = "<h3>Pronto! Como você se sente agora?</h3>";
                }
                time--;
            }, 1000);
        }
        
        function startChatbot() {
            let chatbotDiv = document.getElementById('chatbot');
            chatbotDiv.innerHTML = "<h3>Converse comigo!</h3><p>Como você está se sentindo agora?</p><input type='text' id='userInput' placeholder='Digite aqui...' /><button onclick='replyChatbot()'>Enviar</button><p id='botReply'></p>";
            chatbotDiv.style.display = 'block';
        }
        
        function replyChatbot() {
            let userText = document.getElementById('userInput').value;
            let botReply = document.getElementById('botReply');
            if (userText.toLowerCase().includes('bem') || userText.toLowerCase().includes('melhor')) {
                botReply.innerHTML = "Que ótimo! Continue cuidando do seu bem-estar!";
            } else {
                botReply.innerHTML = "Lembre-se de respirar fundo e focar no presente. Você consegue!";
            }
        }
    </script>
</body>
</html>
