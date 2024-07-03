# UAO

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Aerospace English: Comprehension and Skills Test</title>
    <style>
        :root {
            --primary-color: #3498db;
            --secondary-color: #2c3e50;
            --background-color: #ecf0f1;
            --text-color: #34495e;
            --correct-color: #2ecc71;
            --incorrect-color: #e74c3c;
        }
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            line-height: 1.6;
            color: var(--text-color);
            background-color: var(--background-color);
            padding: 40px;
            max-width: 800px;
            margin: 0 auto;
        }
        .container {
            background-color: white;
            padding: 40px;
            border-radius: 8px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
        h1 {
            text-align: center;
            color: var(--primary-color);
            font-size: 2.5em;
            margin-bottom: 30px;
            border-bottom: 2px solid var(--primary-color);
            padding-bottom: 10px;
        }
        h2 {
            color: var(--secondary-color);
            margin-top: 40px;
            font-size: 1.8em;
            border-left: 4px solid var(--primary-color);
            padding-left: 10px;
        }
        .intro {
            background-color: #f7f9fa;
            padding: 20px;
            margin-bottom: 25px;
            border-radius: 6px;
            border-left: 4px solid var(--primary-color);
        }
        ol {
            margin-bottom: 30px;
            padding-left: 20px;
        }
        li {
            margin-bottom: 20px;
        }
        ol ol {
            list-style-type: none;
            margin-top: 10px;
        }
        ol ol li {
            margin-bottom: 5px;
        }
        .question {
            font-weight: bold;
            margin-bottom: 10px;
        }
        #timer {
            position: fixed;
            top: 20px;
            right: 20px;
            background-color: var(--secondary-color);
            color: white;
            padding: 10px;
            border-radius: 5px;
            font-size: 1.2em;
        }
        .option {
            display: flex;
            align-items: center;
            margin-bottom: 5px;
        }
        .option input {
            margin-right: 10px;
        }
        .correct {
            color: var(--correct-color);
            font-weight: bold;
        }
        .incorrect {
            color: var(--incorrect-color);
            text-decoration: line-through;
        }
        #submit-btn {
            display: block;
            margin: 20px auto;
            padding: 10px 20px;
            font-size: 1.1em;
            background-color: var(--primary-color);
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        #submit-btn:hover {
            background-color: var(--secondary-color);
        }
        #result {
            text-align: center;
            font-size: 1.2em;
            font-weight: bold;
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <div id="timer">15:00</div>
    <div class="container">
        <h1>Aerospace English: Comprehension and Skills Test</h1>

        <form id="quiz-form">
            <h2>Part 1: Misunderstanding</h2>
            <div class="intro">
                <p>Read the following short story and answer the questions:</p>
                <p>John and Maria work at the aerospace base. John asked Maria to "secure the hatch" before leaving. When he returned, he found the hatch open and got angry. Maria was confused because she thought "secure" meant to check that it was working properly.</p>
            </div>
            <ol>
                <li>
                    <div class="question">What was the main cause of the misunderstanding?</div>
                    <ol>
                        <li class="option"><input type="radio" name="q1" value="a"> John didn't give clear instructions</li>
                        <li class="option"><input type="radio" name="q1" value="b"> Maria didn't know what a hatch was</li>
                        <li class="option"><input type="radio" name="q1" value="c"> They interpreted the word "secure" differently</li>
                        <li class="option"><input type="radio" name="q1" value="d"> John forgot to close the hatch himself</li>
                    </ol>
                </li>
                <!-- Add more questions here following the same structure -->
            </ol>
        </form>

        <button id="submit-btn">Submit Answers</button>
        <div id="result"></div>
    </div>

    <script>
        const correctAnswers = {
            q1: 'c',
            // Add correct answers for all questions here
        };

        let timeLeft = 15 * 60; // 15 minutes in seconds
        const timerElement = document.getElementById('timer');

        function updateTimer() {
            const minutes = Math.floor(timeLeft / 60);
            const seconds = timeLeft % 60;
            timerElement.textContent = `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
            
            if (timeLeft > 0) {
                timeLeft--;
                setTimeout(updateTimer, 1000);
            } else {
                submitQuiz();
            }
        }

        updateTimer();

        document.getElementById('submit-btn').addEventListener('click', submitQuiz);

        function submitQuiz() {
            let score = 0;
            const form = document.getElementById('quiz-form');
            const resultDiv = document.getElementById('result');

            for (const question in correctAnswers) {
                const selectedAnswer = form.elements[question].value;
                const correctAnswer = correctAnswers[question];

                const options = form.querySelectorAll(`input[name="${question}"]`);
                options.forEach(option => {
                    option.disabled = true;
                    const listItem = option.parentElement;
                    if (option.value === correctAnswer) {
                        listItem.classList.add('correct');
                    } else if (option.value === selectedAnswer && selectedAnswer !== correctAnswer) {
                        listItem.classList.add('incorrect');
                    }
                });

                if (selectedAnswer === correctAnswer) {
                    score++;
                }
            }

            const totalQuestions = Object.keys(correctAnswers).length;
            resultDiv.textContent = `You scored ${score} out of ${totalQuestions}`;
            
            document.getElementById('submit-btn').disabled = true;
            clearTimeout(updateTimer);
        }
    </script>
</body>
</html>

