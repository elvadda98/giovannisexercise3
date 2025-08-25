<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vocabulary Practice Game - Set 4</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Arial', sans-serif;
            background: linear-gradient(135deg, #8E2DE2 0%, #4A00E0 100%);
            min-height: 100vh;
            padding: 20px;
            color: #333;
        }

        .container {
            max-width: 1000px;
            margin: 0 auto;
            background: white;
            border-radius: 20px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.2);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #8E2DE2, #4A00E0);
            color: white;
            padding: 30px;
            text-align: center;
            position: relative;
        }

        .header::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: url('data:image/svg+xml,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100"><circle cx="20" cy="20" r="2" fill="rgba(255,255,255,0.1)"/><circle cx="80" cy="30" r="1.5" fill="rgba(255,255,255,0.1)"/><circle cx="40" cy="70" r="1" fill="rgba(255,255,255,0.1)"/><circle cx="90" cy="80" r="2.5" fill="rgba(255,255,255,0.1)"/></svg>');
        }

        .header h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
            position: relative;
            z-index: 1;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.2);
        }

        .header p {
            font-size: 1.2em;
            opacity: 0.9;
            position: relative;
            z-index: 1;
        }

        .nav-buttons {
            display: flex;
            justify-content: center;
            gap: 10px;
            padding: 20px;
            background: #f8f9fa;
            flex-wrap: wrap;
        }

        .nav-btn {
            padding: 12px 24px;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
        }

        .nav-btn.active {
            background: linear-gradient(135deg, #8E2DE2, #4A00E0);
            color: white;
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(142,45,226,0.4);
        }

        .nav-btn:not(.active) {
            background: white;
            color: #666;
        }

        .nav-btn:hover:not(.active) {
            background: #e9ecef;
            transform: translateY(-1px);
        }

        .game-section {
            display: none;
            padding: 30px;
            min-height: 400px;
        }

        .game-section.active {
            display: block;
            animation: fadeIn 0.5s ease-in;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .word-bank {
            background: linear-gradient(135deg, #f5f7fa, #e8deff);
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 25px;
            border: 2px solid #8E2DE2;
            box-shadow: 0 4px 15px rgba(142,45,226,0.2);
        }

        .word-bank h3 {
            color: #2c3e50;
            margin-bottom: 15px;
            text-align: center;
            font-size: 1.4em;
        }

        .word-options {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            justify-content: center;
        }

        .word-option {
            background: linear-gradient(135deg, #8E2DE2, #4A00E0);
            color: white;
            padding: 10px 18px;
            border-radius: 20px;
            font-weight: bold;
            font-size: 16px;
            box-shadow: 0 3px 10px rgba(142,45,226,0.3);
            transition: all 0.3s ease;
            cursor: default;
        }

        .word-option:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(142,45,226,0.4);
        }

        .question {
            background: #f8f9fa;
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 20px;
            border-left: 5px solid #8E2DE2;
            box-shadow: 0 4px 15px rgba(0,0,0,0.05);
        }

        .question h3 {
            color: #2c3e50;
            margin-bottom: 15px;
            font-size: 1.3em;
        }

        .fill-blank {
            background: #fff;
            border: 2px solid #ddd;
            border-radius: 8px;
            padding: 8px 12px;
            font-size: 16px;
            margin: 0 5px;
            min-width: 120px;
            transition: border-color 0.3s ease;
        }

        .fill-blank.correct {
            border-color: #4CAF50;
            background: #e8f5e8;
        }

        .fill-blank.incorrect {
            border-color: #f44336;
            background: #ffeaea;
        }

        .options {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-top: 15px;
        }

        .option {
            padding: 15px 20px;
            border: 2px solid #ddd;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: white;
            text-align: center;
            font-weight: 500;
        }

        .option:hover {
            border-color: #8E2DE2;
            transform: translateY(-2px);
            box-shadow: 0 4px 15px rgba(142,45,226,0.2);
        }

        .option.selected {
            background: #8E2DE2;
            color: white;
            border-color: #8E2DE2;
        }

        .option.correct {
            background: #4CAF50;
            color: white;
            border-color: #4CAF50;
        }

        .option.incorrect {
            background: #f44336;
            color: white;
            border-color: #f44336;
        }

        .matching-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin-top: 20px;
        }

        .match-column h4 {
            text-align: center;
            margin-bottom: 15px;
            color: #2c3e50;
            font-size: 1.2em;
        }

        .match-item {
            padding: 15px;
            margin: 8px 0;
            border: 2px solid #ddd;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: white;
            text-align: center;
            font-weight: 500;
        }

        .match-item:hover {
            border-color: #8E2DE2;
            transform: translateY(-1px);
            box-shadow: 0 4px 15px rgba(142,45,226,0.2);
        }

        .match-item.selected {
            background: #f5f7fa;
            border-color: #8E2DE2;
        }

        .match-item.matched {
            background: #4CAF50;
            color: white;
            border-color: #4CAF50;
            cursor: default;
        }

        .check-btn {
            background: linear-gradient(135deg, #8E2DE2, #4A00E0);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            margin: 20px auto;
            display: block;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(142,45,226,0.3);
        }

        .check-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(142,45,226,0.4);
        }

        .feedback {
            margin-top: 15px;
            padding: 15px;
            border-radius: 10px;
            font-weight: bold;
            text-align: center;
            animation: slideIn 0.3s ease;
        }

        @keyframes slideIn {
            from { transform: translateX(-20px); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }

        .feedback.correct {
            background: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }

        .feedback.incorrect {
            background: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
        }

        .score {
            position: fixed;
            top: 20px;
            right: 20px;
            background: linear-gradient(135deg, #8E2DE2, #4A00E0);
            color: white;
            padding: 15px 20px;
            border-radius: 25px;
            font-weight: bold;
            box-shadow: 0 4px 15px rgba(142,45,226,0.3);
            z-index: 1000;
        }

        @media (max-width: 768px) {
            .matching-container {
                grid-template-columns: 1fr;
                gap: 20px;
            }
            
            .nav-buttons {
                flex-direction: column;
                align-items: center;
            }
            
            .nav-btn {
                width: 200px;
            }
            
            .score {
                position: static;
                margin: 20px auto;
                display: block;
                width: fit-content;
            }
        }
    </style>
</head>
<body>
    <div class="score">Score: <span id="score">0</span>/15</div>
    
    <div class="container">
        <div class="header">
            <h1>📚 Vocabulary Builder - Set 4</h1>
            <p>Practice and master these useful English words!</p>
        </div>

        <div class="nav-buttons">
            <button class="nav-btn active" onclick="showSection('fill-gaps')">Fill in the Gaps</button>
            <button class="nav-btn" onclick="showSection('matching')">Match Meanings</button>
            <button class="nav-btn" onclick="showSection('multiple-choice')">Multiple Choice</button>
        </div>

        <!-- Fill in the Gaps Section -->
        <div id="fill-gaps" class="game-section active">
            <div class="word-bank">
                <h3>📝 Word Bank - Choose from these words:</h3>
                <div class="word-options">
                    <span class="word-option">shutters</span>
                    <span class="word-option">wardrobes</span>
                    <span class="word-option">headline</span>
                    <span class="word-option">fall</span>
                    <span class="word-option">deal</span>
                    <span class="word-option">behind</span>
                    <span class="word-option">strike</span>
                    <span class="word-option">wean</span>
                    <span class="word-option">halt</span>
                    <span class="word-option">despite</span>
                    <span class="word-option">somehow</span>
                </div>
            </div>

            <div class="question">
                <h3>Question 1:</h3>
                <p>The construction work came to a <input type="text" class="fill-blank" data-answer="halt" placeholder="answer"> due to heavy rain.</p>
                <div class="feedback" id="feedback-1" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 2:</h3>
                <p>The company is <input type="text" class="fill-blank" data-answer="behind" placeholder="answer"> schedule on the new product launch.</p>
                <div class="feedback" id="feedback-2" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 3:</h3>
                <p>She needed to <input type="text" class="fill-blank" data-answer="wean" placeholder="answer"> her baby from breastfeeding gradually.</p>
                <div class="feedback" id="feedback-3" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 4:</h3>
                <p>The old building began to <input type="text" class="fill-blank" data-answer="fall" placeholder="answer"> apart after years of neglect.</p>
                <div class="feedback" id="feedback-4" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 5:</h3>
                <p>We closed the <input type="text" class="fill-blank" data-answer="shutters" placeholder="answer"> to block out the bright sunlight.</p>
                <div class="feedback" id="feedback-5" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 6:</h3>
                <p>She managed to finish the project <input type="text" class="fill-blank" data-answer="somehow" placeholder="answer">, even with all the difficulties.</p>
                <div class="feedback" id="feedback-6" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 7:</h3>
                <p>The newspaper <input type="text" class="fill-blank" data-answer="headline" placeholder="answer"> announced the election results in bold letters.</p>
                <div class="feedback" id="feedback-7" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 8:</h3>
                <p>The workers decided to <input type="text" class="fill-blank" data-answer="strike" placeholder="answer"> for better working conditions.</p>
                <div class="feedback" id="feedback-8" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 9:</h3>
                <p>They needed to make a <input type="text" class="fill-blank" data-answer="deal" placeholder="answer"> with their suppliers to get better prices.</p>
                <div class="feedback" id="feedback-9" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 10:</h3>
                <p><input type="text" class="fill-blank" data-answer="Despite" placeholder="answer"> his fear of heights, he climbed to the top of the tower.</p>
                <div class="feedback" id="feedback-10" style="display: none;"></div>
            </div>

            <button class="check-btn" onclick="checkFillBlanks()">Check Answers</button>
        </div>

        <!-- Matching Section -->
        <div id="matching" class="game-section">
            <h2 style="text-align: center; margin-bottom: 20px; color: #2c3e50;">Match the words with their meanings</h2>
            <div class="matching-container">
                <div class="match-column">
                    <h4>Words</h4>
                    <div class="match-item" data-word="shutters" onclick="selectMatch(this)">shutters</div>
                    <div class="match-item" data-word="wardrobes" onclick="selectMatch(this)">wardrobes</div>
                    <div class="match-item" data-word="headline" onclick="selectMatch(this)">headline</div>
                    <div class="match-item" data-word="fall" onclick="selectMatch(this)">fall</div>
                    <div class="match-item" data-word="deal" onclick="selectMatch(this)">deal</div>
                    <div class="match-item" data-word="behind" onclick="selectMatch(this)">behind</div>
                    <div class="match-item" data-word="strike" onclick="selectMatch(this)">strike</div>
                    <div class="match-item" data-word="wean" onclick="selectMatch(this)">wean</div>
                    <div class="match-item" data-word="halt" onclick="selectMatch(this)">halt</div>
                    <div class="match-item" data-word="despite" onclick="selectMatch(this)">despite</div>
                    <div class="match-item" data-word="somehow" onclick="selectMatch(this)">somehow</div>
                </div>
                <div class="match-column">
                    <h4>Meanings</h4>
                    <div class="match-item" data-meaning="wean" onclick="selectMatch(this)">to accustom an infant to food other than its mother's milk</div>
                    <div class="match-item" data-meaning="headline" onclick="selectMatch(this)">the title of a newspaper article</div>
                    <div class="match-item" data-meaning="despite" onclick="selectMatch(this)">without being affected by; in spite of</div>
                    <div class="match-item" data-meaning="shutters" onclick="selectMatch(this)">wooden or metal covers on the outside of windows</div>
                    <div class="match-item" data-meaning="fall" onclick="selectMatch(this)">to move downward, typically rapidly and freely</div>
                    <div class="match-item" data-meaning="strike" onclick="selectMatch(this)">to refuse to work as a form of organized protest</div>
                    <div class="match-item" data-meaning="behind" onclick="selectMatch(this)">at or to the far side of something; late in relation to something</div>
                    <div class="match-item" data-meaning="somehow" onclick="selectMatch(this)">in some way; by some means</div>
                    <div class="match-item" data-meaning="halt" onclick="selectMatch(this)">to bring or come to an abrupt stop</div>
                    <div class="match-item" data-meaning="wardrobes" onclick="selectMatch(this)">tall cabinets for storing clothes</div>
                    <div class="match-item" data-meaning="deal" onclick="selectMatch(this)">an agreement entered into by two or more parties</div>
                </div>
            </div>
            <div class="feedback" id="matching-feedback" style="display: none;"></div>
        </div>

        <!-- Multiple Choice Section -->
        <div id="multiple-choice" class="game-section">
            <div class="question">
                <h3>Question 1: What are "shutters" typically used for?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">To store clothes</div>
                    <div class="option" onclick="selectOption(this, false)">To announce news</div>
                    <div class="option" onclick="selectOption(this, true)">To cover windows</div>
                    <div class="option" onclick="selectOption(this, false)">To stop movement</div>
                </div>
                <div class="feedback" id="mc-feedback-1" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 2: Which word means "to stop working as a protest"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">halt</div>
                    <div class="option" onclick="selectOption(this, true)">strike</div>
                    <div class="option" onclick="selectOption(this, false)">wean</div>
                    <div class="option" onclick="selectOption(this, false)">fall</div>
                </div>
                <div class="feedback" id="mc-feedback-2" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 3: "Despite" is used to indicate:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">agreement</div>
                    <div class="option" onclick="selectOption(this, false)">location</div>
                    <div class="option" onclick="selectOption(this, true)">contrast or opposition</div>
                    <div class="option" onclick="selectOption(this, false)">timing</div>
                </div>
                <div class="feedback" id="mc-feedback-3" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 4: Which word refers to tall cabinets for storing clothes?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">shutters</div>
                    <div class="option" onclick="selectOption(this, true)">wardrobes</div>
                    <div class="option" onclick="selectOption(this, false)">deal</div>
                    <div class="option" onclick="selectOption(this, false)">headline</div>
                </div>
                <div class="feedback" id="mc-feedback-4" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 5: What does "wean" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">To stop completely</div>
                    <div class="option" onclick="selectOption(this, false)">To make an agreement</div>
                    <div class="option" onclick="selectOption(this, true)">To gradually accustom to something new</div>
                    <div class="option" onclick="selectOption(this, false)">To move downward</div>
                </div>
                <div class="feedback" id="mc-feedback-5" style="display: none;"></div>
            </div>
        </div>
    </div>

    <script>
        let score = 0;
        let selectedWord = null;
        let selectedMeaning = null;
        let matchedPairs = [];

        function showSection(sectionId) {
            // Hide all sections
            document.querySelectorAll('.game-section').forEach(section => {
                section.classList.remove('active');
            });
            
            // Remove active class from all buttons
            document.querySelectorAll('.nav-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            
            // Show selected section
            document.getElementById(sectionId).classList.add('active');
            
            // Add active class to clicked button
            event.target.classList.add('active');
        }

        function checkFillBlanks() {
            const blanks = document.querySelectorAll('.fill-blank');
            let correctCount = 0;
            
            blanks.forEach((blank, index) => {
                const userAnswer = blank.value.toLowerCase().trim();
                const correctAnswer = blank.dataset.answer.toLowerCase();
                
                if (userAnswer === correctAnswer) {
                    blank.classList.remove('incorrect');
                    blank.classList.add('correct');
                    correctCount++;
                } else {
                    blank.classList.remove('correct');
                    blank.classList.add('incorrect');
                }
            });
            
            // Show feedback for each question
            for (let i = 1; i <= 10; i++) {
                const feedback = document.getElementById(`feedback-${i}`);
                const blank = document.querySelectorAll('.fill-blank')[i - 1];
                
                if (blank.classList.contains('correct')) {
                    feedback.textContent = '✅ Correct!';
                    feedback.className = 'feedback correct';
                } else {
                    feedback.textContent = `❌ Incorrect. The correct answer is: "${blank.dataset.answer}"`;
                    feedback.className = 'feedback incorrect';
                }
                feedback.style.display = 'block';
            }
            
            updateScore();
        }

        function selectMatch(element) {
            if (element.classList.contains('matched')) return;
            
            if (element.dataset.word) {
                // Word selected
                if (selectedWord) selectedWord.classList.remove('selected');
                selectedWord = element;
                element.classList.add('selected');
            } else {
                // Meaning selected
                if (selectedMeaning) selectedMeaning.classList.remove('selected');
                selectedMeaning = element;
                element.classList.add('selected');
            }
            
            // Check if we have both word and meaning selected
            if (selectedWord && selectedMeaning) {
                checkMatch();
            }
        }

        function checkMatch() {
            const feedback = document.getElementById('matching-feedback');
            
            if (selectedWord.dataset.word === selectedMeaning.dataset.meaning) {
                // Correct match
                selectedWord.classList.remove('selected');
                selectedWord.classList.add('matched');
                selectedMeaning.classList.remove('selected');
                selectedMeaning.classList.add('matched');
                
                matchedPairs.push(selectedWord.dataset.word);
                
                feedback.textContent = '✅ Correct match!';
                feedback.className = 'feedback correct';
                
                // Check if all matches are complete
                if (matchedPairs.length === 11) {
                    feedback.textContent = '🎉 Congratulations! You matched all terms correctly!';
                }
            } else {
                // Incorrect match
                feedback.textContent = '❌ Incorrect match. Try again.';
                feedback.className = 'feedback incorrect';
            }
            
            feedback.style.display = 'block';
            selectedWord = null;
            selectedMeaning = null;
            
            updateScore();
        }

        function selectOption(element, isCorrect) {
            // Remove selection from all options in this question
            const options = element.parentElement.querySelectorAll('.option');
            options.forEach(opt => {
                opt.classList.remove('selected');
            });
            
            // Mark the selected option
            element.classList.add('selected');
            
            const questionNumber = element.closest('.question').querySelector('h3').textContent.match(/\d+/)[0];
            const feedback = document.getElementById(`mc-feedback-${questionNumber}`);
            
            if (isCorrect) {
                element.classList.add('correct');
                feedback.textContent = '✅ Correct!';
                feedback.className = 'feedback correct';
            } else {
                element.classList.add('incorrect');
                feedback.textContent = '❌ Incorrect. Try again.';
                feedback.className = 'feedback incorrect';
                
                // Show the correct answer
                options.forEach(opt => {
                    if (opt.onclick.toString().includes('true')) {
                        opt.classList.add('correct');
                    }
                });
            }
            
            feedback.style.display = 'block';
            updateScore();
        }

        function updateScore() {
            // Calculate score for fill-in-the-blank
            let fillScore = 0;
            document.querySelectorAll('.fill-blank.correct').forEach(blank => {
                if (!blank.classList.contains('counted')) {
                    fillScore++;
                    blank.classList.add('counted');
                }
            });
            
            // Calculate score for matching (each pair is 1 point)
            const matchScore = matchedPairs.length;
            
            // Calculate score for multiple choice (each correct is 1 point)
            let mcScore = 0;
            document.querySelectorAll('.option.correct.selected').forEach(opt => {
                mcScore++;
            });
            
            // Total score
            score = fillScore + matchScore + mcScore;
            document.getElementById('score').textContent = score;
        }
    </script>
</body>
</html>
