<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Quiz</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
            background-color: #e0f7fa; /* Azul claro */
            color: #004d40; /* Verde escuro */
        }
        h1 {
            text-align: center;
            color: #00796b; /* Verde */
        }
        .question, .name-input {
            margin-bottom: 20px;
            padding: 15px;
            background-color: #ffffff; /* Branco */
            border: 2px solid #00796b; /* Verde */
            border-radius: 5px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
        }
        .options {
            list-style-type: none;
            padding: 0;
        }
        .options li {
            margin: 5px 0;
        }
        label {
            display: block;
            background-color: #80deea; /* Azul mais claro */
            padding: 10px;
            border-radius: 5px;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        label:hover {
            background-color: #4dd0e1; /* Azul mais escuro */
        }
        #submit {
            background-color: #00796b; /* Verde */
            color: white;
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            display: block;
            margin: 20px auto;
            transition: background-color 0.3s;
        }
        #submit:hover {
            background-color: #004d40; /* Verde escuro */
        }
        #result {
            background-color: #ffffff; /* Branco */
            border: 2px solid #00796b; /* Verde */
            border-radius: 5px;
            padding: 15px;
            text-align: center;
        }
        #start-button {
            background-color: #00796b; /* Verde */
            color: white;
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            display: block;
            margin: 20px auto;
            transition: background-color 0.3s;
        }
        #start-button:hover {
            background-color: #004d40; /* Verde escuro */
        }
    </style>
</head>
<body>

    <h1>Quiz - Teste seus Conhecimentos!</h1>
    <div class="name-input">
        <label for="name">Digite seu nome:</label>
        <input type="text" id="name" placeholder="Seu nome aqui" required>
        <button id="start-button">Iniciar Quiz</button>
    </div>
    <div id="quiz" style="display:none;"></div>
    <button id="submit" style="display:none;">Enviar Respostas</button>
    <div id="result" style="display:none;"></div>

    <script>
        const questions = [
            {
                question: "1. O que é programação?",
                options: ["Escrever historias", "Dar instruções para o computador", "Fazer desenhos no computador", "Digitar textos rapidamente"],
                answer: 1
            },
            {
                question: "2. Como chamamos o comando que faz o computador repetir uma ação?",
                options: ["Repetição", "Pular", "Loop", "Voltar"],
                answer: 2
            },
            {
                question: "3. Qual comando usamos para dizer que o computador só deve fazer algo (se) uma condição for verdadeira?",
                options: ["Sim/não", "Condição", "Talvez", "If"],
                answer: 3
            },
            {
                question: "4. O que é uma variável na programação?",
                options: ["Uma caixinha para guardar informações", "Um comando que repete ações", "Uma função matemática", "Um tipo de erro no programa"],
                answer: 0
            },
            {
                question: "5. Qual é o nome dado às ações que fazemos no teclado ou no mouse para controlar o computador?",
                options: ["Saída", "Programa", "Entrada", "Processador"],
                answer: 2
            },
            {
                question: "6. Como chamamos os erros em um programa de computador?",
                options: ["Bugs", "Problemas", "Variáveis", "Comandos"],
                answer: 0
            },
            {
                question: "7. O que é um algoritmo?",
                options: ["Um tipo de música", "Uma sequência de instruções", "Um personagem de jogo", "Um comando para repetir ações"],
                answer: 1
            },
            {
                question: "8. Como chamamos um bloco de código que faz algo específico em um programa?",
                options: ["Variável", "Condição", "Loop", "Função"],
                answer: 3
            }
        ];

        const quizContainer = document.getElementById('quiz');
        const submitButton = document.getElementById('submit');
        const resultContainer = document.getElementById('result');
        const startButton = document.getElementById('start-button');
        const nameInput = document.getElementById('name');

        function loadQuiz() {
            questions.forEach((q, index) => {
                const questionElement = document.createElement('div');
                questionElement.className = 'question';
                questionElement.innerHTML = `
                    <p>${q.question}</p>
                    <ul class="options">
                        ${q.options.map((option, i) => `
                            <li>
                                <label>
                                    <input type="radio" name="question${index}" value="${i}">
                                    ${option}
                                </label>
                            </li>`).join('')}
                    </ul>
                `;
                quizContainer.appendChild(questionElement);
            });
            submitButton.style.display = 'block';
        }

        function showResult(name) {
            const answers = questions.map((_, index) => {
                const selected = document.querySelector(`input[name="question${index}"]:checked`);
                return selected ? parseInt(selected.value) : -1;
            });

            const score = answers.reduce((acc, answer, index) => 
                acc + (answer === questions[index].answer ? 1 : 0), 0);
            
            resultContainer.innerHTML = `${name}, você acertou ${score} de ${questions.length} perguntas!`;
            resultContainer.style.display = 'block';
        }

        startButton.addEventListener('click', () => {
            const name = nameInput.value.trim();
            if (name) {
                document.querySelector('.name-input').style.display = 'none';
                quizContainer.style.display = 'block';
                loadQuiz();
            } else {
                alert('Por favor, insira seu nome!');
            }
        });

        submitButton.addEventListener('click', () => {
            const name = nameInput.value.trim();
            showResult(name);
        });

    </script>

</body>
</html>
