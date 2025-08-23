<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>English, Aptitude & Python Test</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #6a11cb 0%, #2575fc 100%);
            color: #333;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }
        
        .container {
            background-color: white;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
            width: 90%;
            max-width: 800px;
            overflow: hidden;
        }
        
        header {
            background: linear-gradient(to right, #4b6cb7, #182848);
            color: white;
            padding: 20px;
            text-align: center;
        }
        
        .timer-container {
            background-color: #f5f5f5;
            padding: 10px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 1px solid #ddd;
        }
        
        .timer {
            font-size: 1.2rem;
            font-weight: bold;
            color: #e63946;
        }
        
        .progress-bar {
            height: 10px;
            background-color: #e0e0e0;
            border-radius: 5px;
            overflow: hidden;
            margin: 10px 0;
        }
        
        .progress {
            height: 100%;
            background: linear-gradient(to right, #4caf50, #8bc34a);
            width: 0%;
            transition: width 0.3s ease;
        }
        
        .question-container {
            padding: 20px;
        }
        
        .category {
            color: #4b6cb7;
            font-weight: 600;
            margin-bottom: 5px;
            font-size: 0.9rem;
        }
        
        .question {
            font-size: 1.2rem;
            margin-bottom: 20px;
            line-height: 1.5;
        }
        
        .options {
            display: grid;
            grid-gap: 10px;
            margin-bottom: 20px;
        }
        
        .option {
            padding: 12px 15px;
            background-color: #f8f9fa;
            border: 1px solid #ddd;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.2s ease;
        }
        
        .option:hover {
            background-color: #e9ecef;
            transform: translateY(-2px);
        }
        
        .option.selected {
            background-color: #4b6cb7;
            color: white;
            border-color: #4b6cb7;
        }
        
        .navigation {
            display: flex;
            justify-content: space-between;
            margin-top: 20px;
        }
        
        button {
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-weight: 600;
            transition: all 0.2s ease;
        }
        
        button:disabled {
            opacity: 0.5;
            cursor: not-allowed;
        }
        
        #prev-btn {
            background-color: #6c757d;
            color: white;
        }
        
        #next-btn {
            background-color: #4b6cb7;
            color: white;
        }
        
        #submit-btn {
            background-color: #28a745;
            color: white;
            display: none;
        }
        
        button:hover:not(:disabled) {
            opacity: 0.9;
            transform: scale(1.05);
        }
        
        .result-container {
            padding: 30px;
            text-align: center;
            display: none;
        }
        
        .score {
            font-size: 2rem;
            color: #4b6cb7;
            margin: 20px 0;
        }
        
        .review {
            margin-top: 20px;
            text-align: left;
        }
        
        .review-item {
            margin-bottom: 15px;
            padding: 10px;
            border-radius: 8px;
            background-color: #f8f9fa;
        }
        
        .correct {
            color: #28a745;
        }
        
        .incorrect {
            color: #e63946;
        }
        
        @media (max-width: 600px) {
            .container {
                width: 95%;
            }
            
            .question {
                font-size: 1rem;
            }
            
            .option {
                padding: 10px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>English, Aptitude & Python Test</h1>
            <p>Test your knowledge in three different domains</p>
        </header>
        
        <div class="timer-container">
            <div class="timer">Time Left: <span id="time">15:00</span></div>
            <div>Question <span id="current">1</span> of <span id="total">15</span></div>
        </div>
        
        <div class="progress-bar">
            <div class="progress" id="progress"></div>
        </div>
        
        <div class="question-container" id="question-container">
            <div class="category" id="category">Category</div>
            <div class="question" id="question">Question will be displayed here</div>
            <div class="options" id="options">
                <!-- Options will be inserted here -->
            </div>
            
            <div class="navigation">
                <button id="prev-btn" disabled>Previous</button>
                <button id="next-btn">Next</button>
                <button id="submit-btn">Submit Test</button>
            </div>
        </div>
        
        <div class="result-container" id="result-container">
            <h2>Test Results</h2>
            <div class="score">Your Score: <span id="score-value">0</span>/15</div>
            <p id="result-message">Well done!</p>
            
            <div class="review" id="review">
                <!-- Review content will be inserted here -->
            </div>
            
            <button id="restart-btn" style="margin-top: 20px;">Take Test Again</button>
        </div>
    </div>

    <script>
        // Questions data
        const questions = [
            // English questions
            {
                category: "English",
                question: "Choose the correct synonym for 'Benevolent':",
                options: ["Kind", "Cruel", "Selfish", "Indifferent"],
                answer: 0
            },
            {
                category: "English",
                question: "Which sentence is grammatically correct?",
                options: [
                    "She don't like apples.",
                    "She doesn't likes apples.",
                    "She doesn't like apples.",
                    "She didn't likes apples."
                ],
                answer: 2
            },
            {
                category: "English",
                question: "Identify the figure of speech: 'The stars danced playfully in the moonlit sky.'",
                options: ["Simile", "Metaphor", "Personification", "Hyperbole"],
                answer: 2
            },
            {
                category: "English",
                question: "Which word is spelled correctly?",
                options: ["Occurrence", "Ocurrence", "Occurence", "Ocurrence"],
                answer: 0
            },
            {
                category: "English",
                question: "Choose the correctly punctuated sentence:",
                options: [
                    "The man, who is wearing a blue shirt, is my brother.",
                    "The man who is wearing a blue shirt is my brother.",
                    "The man, who is wearing a blue shirt is my brother.",
                    "The man who is wearing a blue shirt, is my brother."
                ],
                answer: 1
            },
            
            // Aptitude questions
            {
                category: "Aptitude",
                question: "If a train travels 300 km in 5 hours, what is its speed in km/h?",
                options: ["50 km/h", "60 km/h", "55 km/h", "65 km/h"],
                answer: 1
            },
            {
                category: "Aptitude",
                question: "What is 25% of 200?",
                options: ["25", "50", "75", "100"],
                answer: 1
            },
            {
                category: "Aptitude",
                question: "If the pattern is 2, 4, 8, 16, what is the next number?",
                options: ["24", "32", "36", "64"],
                answer: 1
            },
            {
                category: "Aptitude",
                question: "A shirt costs $40 after a 20% discount. What was its original price?",
                options: ["$48", "$50", "$52", "$55"],
                answer: 1
            },
            {
                category: "Aptitude",
                question: "If 3 workers can complete a task in 12 days, how many days will 4 workers take?",
                options: ["8 days", "9 days", "10 days", "16 days"],
                answer: 1
            },
            
            // Python questions
            {
                category: "Python",
                question: "What is the output of 'Hello' + 'World' in Python?",
                options: ["HelloWorld", "Hello World", "Hello+World", "Error"],
                answer: 0
            },
            {
                category: "Python",
                question: "Which keyword is used to define a function in Python?",
                options: ["function", "def", "define", "func"],
                answer: 1
            },
            {
                category: "Python",
                question: "How do you start a for loop in Python?",
                options: [
                    "for i in range(5):",
                    "for (i=0; i<5; i++):",
                    "for i from 0 to 5:",
                    "loop i in range(5):"
                ],
                answer: 0
            },
            {
                category: "Python",
                question: "Which data type is mutable in Python?",
                options: ["Tuple", "String", "List", "Integer"],
                answer: 2
            },
            {
                category: "Python",
                question: "What does the len() function do?",
                options: [
                    "Returns the length of an object",
                    "Returns the largest element",
                    "Returns the smallest element",
                    "Converts to lowercase"
                ],
                answer: 0
            }
        ];

        // Variables to track test state
        let currentQuestion = 0;
        let userAnswers = new Array(questions.length).fill(null);
        let timeLeft = 900; // 15 minutes in seconds
        let timerInterval;

        // DOM elements
        const categoryEl = document.getElementById('category');
        const questionEl = document.getElementById('question');
        const optionsEl = document.getElementById('options');
        const prevBtn = document.getElementById('prev-btn');
        const nextBtn = document.getElementById('next-btn');
        const submitBtn = document.getElementById('submit-btn');
        const currentEl = document.getElementById('current');
        const totalEl = document.getElementById('total');
        const progressEl = document.getElementById('progress');
        const timeEl = document.getElementById('time');
        const questionContainer = document.getElementById('question-container');
        const resultContainer = document.getElementById('result-container');
        const scoreValueEl = document.getElementById('score-value');
        const resultMessageEl = document.getElementById('result-message');
        const reviewEl = document.getElementById('review');
        const restartBtn = document.getElementById('restart-btn');

        // Initialize the test
        function initTest() {
            totalEl.textContent = questions.length;
            showQuestion();
            startTimer();
        }

        // Display current question
        function showQuestion() {
            const question = questions[currentQuestion];
            currentEl.textContent = currentQuestion + 1;
            
            // Update progress bar
            progressEl.style.width = `${((currentQuestion + 1) / questions.length) * 100}%`;
            
            categoryEl.textContent = question.category;
            questionEl.textContent = question.question;
            
            // Clear previous options
            optionsEl.innerHTML = '';
            
            // Add new options
            question.options.forEach((option, index) => {
                const optionEl = document.createElement('div');
                optionEl.classList.add('option');
                if (userAnswers[currentQuestion] === index) {
                    optionEl.classList.add('selected');
                }
                optionEl.textContent = option;
                optionEl.addEventListener('click', () => selectOption(index));
                optionsEl.appendChild(optionEl);
            });
            
            // Update navigation buttons
            prevBtn.disabled = currentQuestion === 0;
            nextBtn.disabled = false;
            
            if (currentQuestion === questions.length - 1) {
                nextBtn.style.display = 'none';
                submitBtn.style.display = 'block';
            } else {
                nextBtn.style.display = 'block';
                submitBtn.style.display = 'none';
            }
        }

        // Select an option
        function selectOption(index) {
            userAnswers[currentQuestion] = index;
            showQuestion();
        }

        // Navigate to previous question
        prevBtn.addEventListener('click', () => {
            if (currentQuestion > 0) {
                currentQuestion--;
                showQuestion();
            }
        });

        // Navigate to next question
        nextBtn.addEventListener('click', () => {
            if (currentQuestion < questions.length - 1) {
                currentQuestion++;
                showQuestion();
            }
        });

        // Submit the test
        submitBtn.addEventListener('click', showResults);

        // Start the timer
        function startTimer() {
            clearInterval(timerInterval);
            timerInterval = setInterval(() => {
                timeLeft--;
                
                const minutes = Math.floor(timeLeft / 60);
                const seconds = timeLeft % 60;
                
                timeEl.textContent = `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
                
                if (timeLeft <= 0) {
                    clearInterval(timerInterval);
                    showResults();
                }
            }, 1000);
        }

        // Show test results
        function showResults() {
            clearInterval(timerInterval);
            
            // Calculate score
            let score = 0;
            questions.forEach((question, index) => {
                if (userAnswers[index] === question.answer) {
                    score++;
                }
            });
            
            // Update results UI
            scoreValueEl.textContent = score;
            
            if (score >= 12) {
                resultMessageEl.textContent = "Excellent job! You have great knowledge in all three areas.";
            } else if (score >= 8) {
                resultMessageEl.textContent = "Good effort! With a bit more practice, you'll master these subjects.";
            } else {
                resultMessageEl.textContent = "Keep practicing! You'll improve with more study and practice.";
            }
            
            // Generate review
            reviewEl.innerHTML = '';
            questions.forEach((question, index) => {
                const reviewItem = document.createElement('div');
                reviewItem.classList.add('review-item');
                
                const isCorrect = userAnswers[index] === question.answer;
                const answerClass = isCorrect ? 'correct' : 'incorrect';
                
                reviewItem.innerHTML = `
                    <p><strong>Q${index + 1}:</strong> ${question.question}</p>
                    <p class="${answerClass}"><strong>Your answer:</strong> ${userAnswers[index] !== null ? question.options[userAnswers[index]] : 'Not answered'}</p>
                    <p class="correct"><strong>Correct answer:</strong> ${question.options[question.answer]}</p>
                `;
                
                reviewEl.appendChild(reviewItem);
            });
            
            // Show results, hide question container
            questionContainer.style.display = 'none';
            resultContainer.style.display = 'block';
        }

        // Restart the test
        restartBtn.addEventListener('click', () => {
            currentQuestion = 0;
            userAnswers = new Array(questions.length).fill(null);
            timeLeft = 900;
            
            questionContainer.style.display = 'block';
            resultContainer.style.display = 'none';
            
            initTest();
        });

        // Initialize the test when page loads
        window.onload = initTest;
    </script>
</body>
</html>
