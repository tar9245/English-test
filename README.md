<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title> Quiz - All Questions</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            background-color: #f0f8ff;
            margin: 0;
            padding: 10px;
            color: #333;
        }
        
        .container {
            max-width: 800px;
            margin: 0 auto;
            background-color: white;
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 0 25px rgba(0, 0, 0, 0.1);
        }
        
        h1 {
            text-align: center;
            color: #2c3e50;
            margin-bottom: 30px;
            border-bottom: 2px solid #3498db;
            padding-bottom: 10px;
        }
        
        .question-container {
            margin-bottom: 25px;
            padding: 20px;
            border: 1px solid #ddd;
            border-radius: 10px;
            background-color: #f9f9f9;
        }
        
        .question {
            font-size: 1.1em;
            margin-bottom: 15px;
            font-weight: bold;
            color: #2c3e50;
        }
        
        .options {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 12px;
        }
        
        .option {
            background-color: #eaf2f8;
            padding: 12px;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.2s;
            border: 2px solid #d4e6f1;
        }
        
        .option:hover {
            background-color: #d4e6f1;
            border-color: #3498db;
        }
        
        .option.selected {
            background-color: #3498db;
            color: white;
            border-color: #2980b9;
        }
        
        .option.correct {
            background-color: #2ecc71;
            color: white;
            border-color: #27ae60;
        }
        
        .option.incorrect {
            background-color: #e74c3c;
            color: white;
            border-color: #c0392b;
        }
        
        .controls {
            text-align: center;
            margin-top: 30px;
        }
        
        button {
            padding: 12px 25px;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-size: 1em;
            transition: all 0.3s;
            background-color: #3498db;
            color: white;
            font-weight: bold;
        }
        
        button:hover {
            background-color: #2980b9;
            transform: translateY(-2px);
            box-shadow: 0 5px 10px rgba(0, 0, 0, 0.1);
        }
        
        button:disabled {
            background-color: #95a5a6;
            cursor: not-allowed;
            transform: none;
            box-shadow: none;
        }
        
        .result {
            text-align: center;
            font-size: 1.5em;
            margin-top: 30px;
            font-weight: bold;
            padding: 20px;
            border-radius: 10px;
            display: none;
        }
        
        .question-number {
            display: inline-block;
            background-color: #3498db;
            color: white;
            width: 30px;
            height: 30px;
            border-radius: 50%;
            text-align: center;
            line-height: 30px;
            margin-right: 10px;
            font-weight: bold;
        }
    </style>
</head>
<body>
	

	
    <div class="container">
        <h1>English Final Exam Test </h1>
<h1>Advanced Level</h1>
        
        <div id="quiz-container">
            <!-- Questions will be inserted here by JavaScript -->
        </div>
        
        <div class="controls">
            <button id="submit-btn">Submit Answers</button>
        </div>
        
        <div class="result" id="result"></div>
    </div>

    <script>
        // Quiz questions (10 math questions)
        const quizQuestions = [
            {
                question: "If you don't study your homework right now, the math teacher_____ get angry at you.",
                options: ["will be", "will", "would", "what"],
                answer: 1
            },
            {
                question: "When Eh War Phaw woke up in the morning and ______ the window, she saw a handsome boy.",
                options: ["open", "opened", "opening", "oggy"],
                answer: 1
            },
            {
                question: "G12 Students_____very intelligent.",
                options: ["are", "is", "are not", "and"],
                answer: 0
                
            },
            {
                question: "I like her.But i don't _____any money.",
                options: ["have", "has", "had", "hat"],
                answer: 0
            },
            {
                question: "I have ever _____to myanmar.",
                options: ["be", "go", "been", "bean"],
                answer: 2
            },
            
                
        ];
        
        // Quiz state
        let selectedAnswers = Array(quizQuestions.length).fill(null);
        let quizSubmitted = false;
        
        // DOM elements
        const quizContainer = document.getElementById('quiz-container');
        const submitBtn = document.getElementById('submit-btn');
        const resultDiv = document.getElementById('result');
        
        // Initialize quiz
        function initQuiz() {
            // Create all question elements
            quizQuestions.forEach((question, qIndex) => {
                const questionDiv = document.createElement('div');
                questionDiv.className = 'question-container';
                
                // Add question number and text
                const questionText = document.createElement('div');
                questionText.className = 'question';
                questionText.innerHTML = `<span class="question-number">${qIndex + 1}</span>${question.question}`;
                questionDiv.appendChild(questionText);
                
                // Add options container
                const optionsDiv = document.createElement('div');
                optionsDiv.className = 'options';
                
                // Add each option
                question.options.forEach((option, oIndex) => {
                    const optionElement = document.createElement('div');
                    optionElement.className = 'option';
                    optionElement.textContent = option;
                    
                    optionElement.addEventListener('click', () => selectAnswer(qIndex, oIndex));
                    optionsDiv.appendChild(optionElement);
                });
                
                questionDiv.appendChild(optionsDiv);
                quizContainer.appendChild(questionDiv);
            });
        }
        
        // Select an answer
        function selectAnswer(qIndex, oIndex) {
            if (quizSubmitted) return;
            
            // Clear previous selection for this question
            const questionDiv = quizContainer.children[qIndex];
            const options = questionDiv.querySelectorAll('.option');
            options.forEach(opt => opt.classList.remove('selected'));
            
            // Select new answer
            options[oIndex].classList.add('selected');
            selectedAnswers[qIndex] = oIndex;
        }
        
        // Submit quiz
        submitBtn.addEventListener('click', () => {
            // Check if all questions are answered
            if (selectedAnswers.includes(null)) {
                alert("မေးခွန်းတွေအကုန်လုံးဖြေပြီးမှsubmitနိပ်ကြပါဗျား");
                return;
            }
            
            quizSubmitted = true;
            submitBtn.disabled = true;
            
            // Calculate score
            let score = 0;
            quizQuestions.forEach((question, index) => {
                if (selectedAnswers[index] === question.answer) {
                    score++;
                }
            });
            
            // Display result
            resultDiv.style.display = 'block';
            resultDiv.textContent = `You scored ${score} out of ${quizQuestions.length}!`;
            
            // Color based on performance
            if (score === quizQuestions.length) {
                resultDiv.style.backgroundColor = '#d5f5e3';
                resultDiv.style.color = '#27ae60';
            } else if (score >= quizQuestions.length * 0.7) {
                resultDiv.style.backgroundColor = '#d6eaf8';
                resultDiv.style.color = '#2980b9';
            } else {
                resultDiv.style.backgroundColor = '#fadbd8';
                resultDiv.style.color = '#c0392b';
            }
            
            // Show correct/incorrect answers
            quizQuestions.forEach((question, qIndex) => {
                const questionDiv = quizContainer.children[qIndex];
                const options = questionDiv.querySelectorAll('.option');
                
                options.forEach((option, oIndex) => {
                    if (oIndex === question.answer) {
                        option.classList.add('correct');
                    } else if (selectedAnswers[qIndex] === oIndex && oIndex !== question.answer) {
                        option.classList.add('incorrect');
                    }
                });
            });
        });
        
        // Start the quiz
        initQuiz();
    </script>
</body>
</html>
