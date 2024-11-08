<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Quiz Game for Kids</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f9f9f9;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            min-height: 100vh;
            margin: 0;
        }
        .quiz-container {
            background: #fff;
            border-radius: 8px;
            padding: 20px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            max-width: 400px;
            text-align: center;
        }
        h1 {
            color: #333;
        }
        .question {
            font-size: 1.2em;
            margin-bottom: 15px;
        }
        .choices {
            list-style: none;
            padding: 0;
        }
        .choices li {
            background: #e0f7fa;
            margin: 5px 0;
            padding: 10px;
            border-radius: 5px;
            cursor: pointer;
        }
        .choices li:hover {
            background: #b2ebf2;
        }
        .score {
            font-size: 1.2em;
            color: #4caf50;
            margin-top: 15px;
        }
        .high-score {
            color: #ff9800;
            margin-top: 10px;
        }
        .next-button {
            padding: 10px 20px;
            margin-top: 15px;
            background-color: #4caf50;
            color: #fff;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        .next-button:hover {
            background-color: #388e3c;
        }
    </style>
</head>
<body>
    <div class="quiz-container">
        <h1>Quiz Game for Kids</h1>
        <div id="high-score" class="high-score"></div>
        <div id="question-container">
            <p id="question" class="question"></p>
            <ul id="choices" class="choices"></ul>
        </div>
        <p id="score" class="score"></p>
        <button id="next" class="next-button" onclick="nextQuestion()" style="display: none;">Next Question</button>
    </div>

    <script>
        const questions = [
            { question: "What is the capital of France?", choices: ["Berlin", "Madrid", "Paris", "Rome"], answer: 2 },
            { question: "Which planet is known as the Red Planet?", choices: ["Earth", "Mars", "Jupiter", "Venus"], answer: 1 },
            { question: "What is the tallest mountain in the world?", choices: ["Mount Kilimanjaro", "Mount Everest", "K2", "Mount Fuji"], answer: 1 },
            { question: "Who is known as the Father of Computers?", choices: ["Charles Babbage", "Alan Turing", "Thomas Edison", "Nikola Tesla"], answer: 0 },
            { question: "What is the freezing point of water in Celsius?", choices: ["0", "-10", "32", "-32"], answer: 0 }
        ];

        let currentQuestion = 0;
        let score = 0;
        let highScore = 0;

        const questionElement = document.getElementById("question");
        const choicesElement = document.getElementById("choices");
        const scoreElement = document.getElementById("score");
        const highScoreElement = document.getElementById("high-score");
        const nextButton = document.getElementById("next");

        function loadQuestion() {
            questionElement.textContent = `Question ${currentQuestion + 1}: ${questions[currentQuestion].question}`;
            choicesElement.innerHTML = "";

            questions[currentQuestion].choices.forEach((choice, index) => {
                const choiceElement = document.createElement("li");
                choiceElement.textContent = choice;
                choiceElement.onclick = () => checkAnswer(index);
                choicesElement.appendChild(choiceElement);
            });

            nextButton.style.display = "none";
            scoreElement.textContent = "";
        }

        function checkAnswer(selected) {
            const correct = questions[currentQuestion].answer;
            if (selected === correct) {
                score++;
                scoreElement.textContent = "Correct!";
            } else {
                scoreElement.textContent = `Incorrect. The correct answer was ${questions[currentQuestion].choices[correct]}.`;
            }

            nextButton.style.display = "block";
        }

        function nextQuestion() {
            currentQuestion++;
            if (currentQuestion < questions.length) {
                loadQuestion();
            } else {
                endQuiz();
            }
        }

        function endQuiz() {
            if (score > highScore) {
                highScore = score;
                highScoreElement.textContent = `New High Score: ${highScore}`;
            } else {
                highScoreElement.textContent = `High Score: ${highScore}`;
            }

            questionElement.textContent = `Quiz Finished! Your score is: ${score}/${questions.length}`;
            choicesElement.innerHTML = "";
            nextButton.style.display = "none";
            score = 0;
            currentQuestion = 0;
            setTimeout(loadQuestion, 3000);
        }

        loadQuestion();
    </script>
</body>
</html>

