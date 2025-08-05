<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>TEA Framework - Interactive Games</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            background: white;
            border-radius: 15px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.1);
            overflow: hidden;
            min-height: 80vh;
        }
        
        .header {
            background: linear-gradient(135deg, #2c3e50 0%, #34495e 100%);
            color: white;
            padding: 30px;
            text-align: center;
        }
        
        .logo-container {
            margin: 0 auto 20px;
            display: flex;
            align-items: center;
            justify-content: center;
            max-width: 300px;
        }
        
        .header h1 {
            font-size: 2.2em;
            margin-bottom: 10px;
            font-weight: 300;
        }
        
        .header p {
            font-size: 1.1em;
            opacity: 0.9;
        }
        
        .content {
            padding: 30px;
        }
        
        .screen {
            display: none;
        }
        
        .screen.active {
            display: block;
        }
        
        /* Home Screen */
        .home-screen {
            text-align: center;
        }
        
        .player-setup {
            background: #f8f9fa;
            padding: 30px;
            border-radius: 10px;
            margin-bottom: 30px;
        }
        
        .player-input {
            display: flex;
            gap: 15px;
            justify-content: center;
            align-items: center;
            margin-bottom: 20px;
            flex-wrap: wrap;
        }
        
        .player-input input {
            padding: 12px 20px;
            border: 2px solid #e1e5e9;
            border-radius: 25px;
            font-size: 16px;
            min-width: 200px;
        }
        
        .btn {
            padding: 12px 24px;
            border: none;
            border-radius: 25px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
            font-size: 16px;
        }
        
        .btn-primary {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
        }
        
        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(102, 126, 234, 0.3);
        }
        
        .btn-success {
            background: linear-gradient(135deg, #00b894 0%, #00a085 100%);
            color: white;
        }
        
        .btn-danger {
            background: linear-gradient(135deg, #e17055 0%, #d63031 100%);
            color: white;
        }
        
        .games-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
            margin-top: 30px;
        }
        
        .game-card {
            background: linear-gradient(135deg, #74b9ff 0%, #0984e3 100%);
            color: white;
            padding: 30px;
            border-radius: 15px;
            text-align: center;
            cursor: pointer;
            transition: transform 0.3s;
        }
        
        .game-card:hover {
            transform: translateY(-5px);
        }
        
        .game-card h3 {
            font-size: 1.5em;
            margin-bottom: 15px;
        }
        
        .game-card p {
            opacity: 0.9;
            margin-bottom: 20px;
        }
        
        /* Game Screens */
        .game-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 30px;
            flex-wrap: wrap;
            gap: 15px;
        }
        
        .player-info {
            background: linear-gradient(135deg, #fd79a8 0%, #e84393 100%);
            color: white;
            padding: 15px 25px;
            border-radius: 25px;
            font-weight: 600;
        }
        
        .score-info {
            background: linear-gradient(135deg, #00b894 0%, #00a085 100%);
            color: white;
            padding: 15px 25px;
            border-radius: 25px;
            font-weight: 600;
        }
        
        .progress-bar {
            background: #ecf0f1;
            border-radius: 10px;
            height: 20px;
            margin: 20px 0;
            overflow: hidden;
        }
        
        .progress-fill {
            background: linear-gradient(135deg, #00b894 0%, #00a085 100%);
            height: 100%;
            transition: width 0.3s;
            border-radius: 10px;
        }
        
        /* Matching Game */
        .matching-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin: 20px 0;
        }
        
        .terms-column, .definitions-column {
            background: #f8f9fa;
            padding: 20px;
            border-radius: 10px;
        }
        
        .match-item {
            background: white;
            padding: 15px;
            margin: 10px 0;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.3s;
            border: 2px solid transparent;
        }
        
        .match-item:hover {
            transform: translateX(5px);
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }
        
        .match-item.selected {
            border-color: #3498db;
            background: #e3f2fd;
        }
        
        .match-item.correct {
            border-color: #27ae60;
            background: #d5f4e6;
        }
        
        .match-item.incorrect {
            border-color: #e74c3c;
            background: #fdeaea;
        }
        
        .match-item.disabled {
            opacity: 0.5;
            cursor: not-allowed;
            background: #f5f5f5;
        }
        
        /* Sorting Game */
        .sorting-container {
            margin: 20px 0;
        }
        
        .categories {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }
        
        .category-box {
            background: #f8f9fa;
            border: 2px dashed #bdc3c7;
            border-radius: 10px;
            padding: 20px;
            min-height: 150px;
            transition: all 0.3s;
        }
        
        .category-box.drag-over {
            border-color: #3498db;
            background: #e3f2fd;
        }
        
        .category-title {
            text-align: center;
            font-weight: 600;
            color: #2c3e50;
            margin-bottom: 15px;
            padding: 10px;
            background: white;
            border-radius: 5px;
        }
        
        .sortable-items {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            justify-content: center;
            margin-bottom: 20px;
        }
        
        .sortable-item {
            background: white;
            padding: 12px 18px;
            border-radius: 20px;
            cursor: grab;
            transition: all 0.3s;
            border: 2px solid #e1e5e9;
            font-size: 14px;
        }
        
        .sortable-item:hover {
            transform: scale(1.05);
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }
        
        .sortable-item.dragging {
            opacity: 0.5;
            cursor: grabbing;
        }
        
        /* Results and Leaderboard */
        .results-container {
            text-align: center;
        }
        
        .final-score {
            background: linear-gradient(135deg, #f39c12 0%, #e67e22 100%);
            color: white;
            padding: 30px;
            border-radius: 15px;
            margin: 20px 0;
        }
        
        .final-score h2 {
            font-size: 2.5em;
            margin-bottom: 10px;
        }
        
        .leaderboard {
            background: #f8f9fa;
            border-radius: 10px;
            padding: 25px;
            margin: 20px 0;
        }
        
        .leaderboard h3 {
            color: #2c3e50;
            margin-bottom: 20px;
            font-size: 1.5em;
        }
        
        .leaderboard-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px;
            margin: 10px 0;
            background: white;
            border-radius: 8px;
            border-left: 4px solid #3498db;
        }
        
        .leaderboard-item.top-score {
            border-left-color: #f39c12;
            background: linear-gradient(135deg, #fff5e6 0%, #ffecd2 100%);
        }
        
        .rank {
            font-weight: bold;
            color: #2c3e50;
            font-size: 1.2em;
        }
        
        .player-name {
            font-weight: 600;
            color: #2c3e50;
        }
        
        .player-score {
            font-weight: bold;
            color: #27ae60;
            font-size: 1.1em;
        }
        
        .answers-section {
            background: #f8f9fa;
            border-radius: 10px;
            padding: 25px;
            margin: 20px 0;
            text-align: left;
        }
        
        .answer-item {
            background: white;
            padding: 15px;
            margin: 10px 0;
            border-radius: 8px;
            border-left: 4px solid #27ae60;
        }
        
        .answer-term {
            font-weight: bold;
            color: #2c3e50;
            margin-bottom: 5px;
        }
        
        .answer-definition {
            color: #636e72;
            line-height: 1.5;
        }
        
        @media (max-width: 768px) {
            .content {
                padding: 15px;
            }
            
            .matching-container {
                grid-template-columns: 1fr;
            }
            
            .game-header {
                flex-direction: column;
                text-align: center;
            }
            
            .categories {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <div class="logo-container">
                <svg viewBox="0 0 1200 350" xmlns="http://www.w3.org/2000/svg">
                    <g>
                        <path d="M50 50 L200 50 L125 200 Z" fill="url(#grad1)" />
                        <path d="M80 80 L170 80 L125 170 Z" fill="white" />
                        <path d="M100 100 L150 100 L125 150 Z" fill="url(#grad2)" />
                    </g>
                    <text x="250" y="140" font-family="Arial, sans-serif" font-size="120" font-weight="bold" fill="url(#textGrad)">TPI-US</text>
                    <text x="250" y="190" font-family="Arial, sans-serif" font-size="24" font-weight="normal" fill="#2E86AB" letter-spacing="3px">IDENTIFY • IMPLEMENT • IMPACT</text>
                    <defs>
                        <linearGradient id="grad1" x1="0%" y1="0%" x2="100%" y2="100%">
                            <stop offset="0%" style="stop-color:#8B5A96;stop-opacity:1" />
                            <stop offset="100%" style="stop-color:#2E86AB;stop-opacity:1" />
                        </linearGradient>
                        <linearGradient id="grad2" x1="0%" y1="0%" x2="100%" y2="100%">
                            <stop offset="0%" style="stop-color:#6A4C93;stop-opacity:1" />
                            <stop offset="100%" style="stop-color:#2E86AB;stop-opacity:1" />
                        </linearGradient>
                        <linearGradient id="textGrad" x1="0%" y1="0%" x2="100%" y2="0%">
                            <stop offset="0%" style="stop-color:#5D2E5D;stop-opacity:1" />
                            <stop offset="50%" style="stop-color:#2E4C96;stop-opacity:1" />
                            <stop offset="100%" style="stop-color:#2E86AB;stop-opacity:1" />
                        </linearGradient>
                    </defs>
                </svg>
            </div>
            <h1>TEA Framework Interactive Games</h1>
            <p>Multiplayer Learning Activities - Play Independently and Compare Scores!</p>
        </div>
        
        <div class="content">
            <!-- Home Screen -->
            <div id="homeScreen" class="screen active">
                <div class="home-screen">
                    <div class="player-setup">
                        <h2>Welcome! Choose Your Play Style</h2>
                        
                        <div style="display: flex; gap: 20px; justify-content: center; margin-bottom: 30px; flex-wrap: wrap;">
                            <button class="btn btn-primary" onclick="showIndividualSetup()">Play as Individual</button>
                            <button class="btn btn-success" onclick="showTeamSetup()">Play as Team</button>
                        </div>
                        
                        <!-- Individual Setup -->
                        <div id="individualSetup" style="display: none;">
                            <h3>Individual Player Setup</h3>
                            <div class="player-input">
                                <input type="text" id="playerName" placeholder="Enter your name..." maxlength="20">
                                <button class="btn btn-primary" onclick="setPlayerName()">Set Name</button>
                            </div>
                        </div>
                        
                        <!-- Team Setup -->
                        <div id="teamSetup" style="display: none;">
                            <h3>Team Player Setup</h3>
                            <div class="player-input">
                                <select id="teamSelect" style="padding: 12px 20px; border: 2px solid #e1e5e9; border-radius: 25px; font-size: 16px; min-width: 200px;">
                                    <option value="">Select Your Team</option>
                                    <option value="Table 5: Brittany">Table 5: Brittany</option>
                                    <option value="Table 9: Holly & Yo">Table 9: Holly & Yo</option>
                                </select>
                                <input type="text" id="teamPlayerName" placeholder="Your name..." maxlength="20">
                                <button class="btn btn-success" onclick="setTeamPlayer()">Join Team</button>
                            </div>
                            <div id="teamMembers" style="margin-top: 20px; font-size: 0.9em; color: #666;"></div>
                        </div>
                        
                        <div id="playerGreeting" style="display: none;">
                            <h3>Welcome, <span id="currentPlayerName"></span>! Choose a game to play:</h3>
                        </div>
                    </div>
                    
                    <div class="games-grid" id="gamesGrid" style="display: none;">
                        <div class="game-card" onclick="startGame('matching')">
                            <h3>🎯 Term Matching</h3>
                            <p>Match TEA Framework terms with their definitions</p>
                            <div class="btn btn-success">Play Now</div>
                        </div>
                        
                        <div class="game-card" onclick="startGame('sorting')">
                            <h3>📊 Category Sorting</h3>
                            <p>Sort terms into correct framework categories</p>
                            <div class="btn btn-success">Play Now</div>
                        </div>
                        
                        <div class="game-card" onclick="startGame('frameworkQuestions')">
                            <h3>❓ Framework Questions</h3>
                            <p>Match essential questions to their framework areas</p>
                            <div class="btn btn-success">Play Now</div>
                        </div>
                        
                        <div class="game-card" onclick="showLeaderboard()">
                            <h3>🏆 Leaderboard</h3>
                            <p>See top scores and correct answers</p>
                            <div class="btn btn-primary">View Results</div>
                        </div>
                    </div>
                </div>
            </div>
            
            <!-- Matching Game Screen -->
            <div id="matchingScreen" class="screen">
                <div class="game-header">
                    <div class="player-info">Player: <span id="matchingPlayerName"></span></div>
                    <div class="score-info">Score: <span id="matchingScore">0</span></div>
                    <button class="btn btn-danger" onclick="goHome()">Exit Game</button>
                </div>
                
                <div class="progress-bar">
                    <div class="progress-fill" id="matchingProgress"></div>
                </div>
                
                <h2>Match Terms with Definitions</h2>
                <p>Click a term, then click its matching definition</p>
                
                <div class="matching-container">
                    <div class="terms-column">
                        <h3>Terms</h3>
                        <div id="termsContainer"></div>
                    </div>
                    <div class="definitions-column">
                        <h3>Definitions</h3>
                        <div id="definitionsContainer"></div>
                    </div>
                </div>
                
                <div style="text-align: center; margin-top: 20px;">
                    <button class="btn btn-primary" id="submitMatching" onclick="submitMatching()" disabled>Submit Answers</button>
                </div>
            </div>
            
            <!-- Sorting Game Screen -->
            <div id="sortingScreen" class="screen">
                <div class="game-header">
                    <div class="player-info">Player: <span id="sortingPlayerName"></span></div>
                    <div class="score-info">Score: <span id="sortingScore">0</span></div>
                    <button class="btn btn-danger" onclick="goHome()">Exit Game</button>
                </div>
                
                <h2>Sort Terms by Framework Area</h2>
                <p>Drag terms into the correct framework categories</p>
                
                <div class="sortable-items" id="sortableItems"></div>
                
                <div class="categories">
                    <div class="category-box" data-category="training">
                        <div class="category-title">Quality of Candidate Training</div>
                        <div class="drop-zone" id="training-zone"></div>
                    </div>
                    <div class="category-box" data-category="practice">
                        <div class="category-title">Quality of Practice</div>
                        <div class="drop-zone" id="practice-zone"></div>
                    </div>
                    <div class="category-box" data-category="support">
                        <div class="category-title">Quality of Candidate Support</div>
                        <div class="drop-zone" id="support-zone"></div>
                    </div>
                </div>
                
                <div style="text-align: center; margin-top: 20px;">
                    <button class="btn btn-primary" onclick="submitSorting()">Submit Answers</button>
                </div>
            </div>
            
            <!-- Quick Match Screen -->
            <div id="quickMatchScreen" class="screen">
                <div class="game-header">
                    <div class="player-info">Player: <span id="quickMatchPlayerName"></span></div>
                    <div class="score-info">Score: <span id="quickMatchScore">0</span> | Time: <span id="timeLeft">60</span>s</div>
                    <button class="btn btn-danger" onclick="goHome()">Exit Game</button>
                </div>
                
                <h2>Quick Match Challenge</h2>
                <p>Match as many as you can before time runs out!</p>
                
                <div class="matching-container">
                    <div class="terms-column">
                        <h3>Term</h3>
                        <div id="quickTermContainer"></div>
                    </div>
                    <div class="definitions-column">
                        <h3>Choose the Correct Definition</h3>
                        <div id="quickDefinitionsContainer"></div>
                    </div>
                </div>
            </div>
            
            <!-- Results Screen -->
            <div id="resultsScreen" class="screen">
                <div class="results-container">
                    <div class="final-score">
                        <h2>Game Complete!</h2>
                        <div>Your Score: <span id="finalScore"></span>%</div>
                        <div>Game: <span id="gameType"></span></div>
                    </div>
                    
                    <div class="leaderboard">
                        <h3>🏆 Leaderboard</h3>
                        <div id="leaderboardContainer"></div>
                    </div>
                    
                    <div class="answers-section">
                        <h3>📚 Correct Answers</h3>
                        <div id="answersContainer"></div>
                    </div>
                    
                    <div style="text-align: center; margin-top: 30px;">
                        <button class="btn btn-primary" onclick="goHome()">Back to Games</button>
                        <button class="btn btn-success" onclick="saveResults()">Save My Score</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
    
    <script>
        // Game Data from TEA Framework Glossary and Essential Questions
        const gameData = {
            matching: [
                {
                    term: "Academic Feedback",
                    definition: "Feedback provided to students that is timely, accurate, and specific, used to assess progress and improve understanding"
                },
                {
                    term: "Differentiation",
                    definition: "Tailoring instruction to meet the needs of all students by varying content, process, products, or learning environment"
                },
                {
                    term: "Behavior Management",
                    definition: "Clear rules and expectations for learning and behavior that are explicitly established and positively reinforced"
                },
                {
                    term: "Questioning",
                    definition: "Purposeful, differentiated questions aligned to objectives and varied in level to elicit student thinking"
                },
                {
                    term: "Science of Reading",
                    definition: "Research-based approach supporting explicit, systematic, and sequential instruction in all five reading components"
                },
                {
                    term: "Student Engagement",
                    definition: "Students actively contributing to learning through discussion, questioning, and meaningful participation"
                },
                {
                    term: "Assessment",
                    definition: "Formative and summative evaluation used to inform instructional decisions and guide student learning"
                },
                {
                    term: "High-Quality Feedback",
                    definition: "Timely, accurate, and specific feedback that focuses on learning rather than being 'right' or 'wrong'"
                },
                {
                    term: "Preparation for Effective Instruction",
                    definition: "Does EPP coursework strategically incorporate key components that foster strong preparation and delivery?"
                },
                {
                    term: "Content Pedagogy Knowledge in Reading",
                    definition: "Does the EPP provide comprehensive training in literacy content pedagogy and Science of Teaching Reading?"
                },
                {
                    term: "Content Pedagogy Knowledge in Math",
                    definition: "Does the EPP provide comprehensive training in math content pedagogy with evidence-based instruction?"
                },
                {
                    term: "Pedagogical Preparation for All Learners",
                    definition: "Does EPP coursework equip candidates with knowledge, strategies, and mindsets to reach all learners?"
                },
                {
                    term: "Selection of Field Personnel",
                    definition: "Does the EPP uphold high standards by implementing rigorous selection process for supervisors and teachers?"
                },
                {
                    term: "Practice-Based Experiences",
                    definition: "Does the EPP ensure high-quality preparation through structured, practice-based experiences bridging theory and application?"
                },
                {
                    term: "Quality of Clinical Placements",
                    definition: "Does the EPP ensure clinical placements are collaboratively designed, appropriately matched, and sufficiently timed?"
                },
                {
                    term: "Data Driven Decision-Making",
                    definition: "Does the EPP systematically collaborate with P-12 partners to ensure high-quality placements and recruitment?"
                }
            ],
            
            sorting: [
                {
                    term: "Evidence-based instructional strategies",
                    category: "training"
                },
                {
                    term: "High-quality instructional materials (HQIM)",
                    category: "training"
                },
                {
                    term: "Science of Teaching Reading",
                    category: "training"
                },
                {
                    term: "Math content pedagogy",
                    category: "training"
                },
                {
                    term: "Evaluation of quality and delivery",
                    category: "training"
                },
                {
                    term: "Pedagogical preparation for all learners",
                    category: "training"
                },
                {
                    term: "Clinical placement selection",
                    category: "practice"
                },
                {
                    term: "Practice-based experiences",
                    category: "practice"
                },
                {
                    term: "Cooperating teacher selection",
                    category: "practice"
                },
                {
                    term: "Data-driven decision making",
                    category: "practice"
                },
                {
                    term: "Quality of clinical placements",
                    category: "practice"
                },
                {
                    term: "P-12 collaboration",
                    category: "practice"
                },
                {
                    term: "Field supervisor training",
                    category: "support"
                },
                {
                    term: "Observation and feedback systems",
                    category: "support"
                },
                {
                    term: "Candidate performance monitoring",
                    category: "support"
                },
                {
                    term: "Intervention support plans",
                    category: "support"
                },
                {
                    term: "Quality of coaching and feedback",
                    category: "support"
                },
                {
                    term: "Candidate proficiency and readiness",
                    category: "support"
                }
            ],
            
            frameworkQuestions: [
                {
                    question: "To what extent does EPP coursework strategically incorporate the key components that foster strong preparation and delivery?",
                    area: "Quality of Candidate Training - Preparation for Effective Instruction"
                },
                {
                    question: "To what extent does the EPP provide comprehensive training in literacy content pedagogy and the Science of Teaching Reading instruction?",
                    area: "Quality of Candidate Training - Content Pedagogy Knowledge in Reading"
                },
                {
                    question: "To what extent does the EPP provide comprehensive training in math content pedagogy?",
                    area: "Quality of Candidate Training - Content Pedagogy Knowledge in Math"
                },
                {
                    question: "To what extent does EPP coursework and training equip candidates with the knowledge, strategies, and mindsets to reach all learners?",
                    area: "Quality of Candidate Training - Pedagogical Preparation for All Learners"
                },
                {
                    question: "To what extent does the EPP systematically evaluate the design, rigor, and delivery of content across all coursework and clinical practice?",
                    area: "Quality of Candidate Training - Evaluation of Quality and Delivery"
                },
                {
                    question: "To what extent does the EPP uphold high standards of quality by implementing a rigorous and collaborative selection process for field supervisors and clinical support teachers?",
                    area: "Quality of Practice - Selection of Field Personnel"
                },
                {
                    question: "To what extent does the EPP ensure high-quality preparation through structured, practice-based experiences that bridge theory and real-world application?",
                    area: "Quality of Practice - Practice-Based Experiences"
                },
                {
                    question: "To what extent does the EPP ensure that clinical placements are collaboratively designed, appropriately matched, and sufficiently timed to support meaningful candidate development?",
                    area: "Quality of Practice - Quality of Clinical Placements"
                },
                {
                    question: "To what extent does the EPP systematically collaborate with P-12 partners to ensure high-quality clinical placements and responsive recruitment strategies?",
                    area: "Quality of Practice - Data Driven Decision-Making with P-12 Partners"
                },
                {
                    question: "To what extent does the EPP ensure that faculty, field supervisors, and clinical support teachers receive consistent preparation, ongoing calibration, and targeted professional development to support candidate growth?",
                    area: "Quality of Candidate Support - Training and Support of Personnel"
                },
                {
                    question: "To what extent does the EPP ensure that observation and feedback systems focus on key instructional practices and provide evidence-based, actionable support that strengthens candidate effectiveness and student learning?",
                    area: "Quality of Candidate Support - Quality of Coaching and Feedback"
                },
                {
                    question: "To what extent does the EPP ensure, through data usage, that it supports teacher candidates to meet clearly defined performance standards through ongoing assessment, targeted feedback, and structured interventions that strengthen instructional practice and advance student learning?",
                    area: "Quality of Candidate Support - Candidate Proficiency and Readiness Over Time"
                }
            ]
        };
        
        // Game State
        let currentPlayer = '';
        let currentTeam = '';
        let isTeamMode = false;
        let gameState = {
            selectedTerm: null,
            selectedDefinition: null,
            matches: new Map(),
            score: 0,
            currentGame: null,
            timeLeft: 60,
            quickMatchIndex: 0,
            attempts: new Map(),
            maxAttempts: 2
        };
        
        // Team data
        const teamData = {
            "Table 5: Brittany": [
                "Amy Barrios",
                "Victor Favela", 
                "Teresa Hinojos",
                "Liza LaRue",
                "Bethany LaPla"
            ],
            "Table 9: Holly & Yo": [
                "Erica Orozco",
                "Shaleka Boone", 
                "Jessica McLoughin"
            ]
        };
        
        // Local Storage for scores
        function getScores() {
            return JSON.parse(localStorage.getItem('teaFrameworkScores')) || [];
        }
        
        function saveScore(playerName, gameType, score, total) {
            const scores = getScores();
            const percentage = Math.round((score / total) * 100);
            const playerDisplay = isTeamMode ? `${playerName} (${currentTeam})` : playerName;
            
            scores.push({
                player: playerDisplay,
                team: currentTeam,
                game: gameType,
                score: percentage,
                date: new Date().toISOString(),
                correct: score,
                total: total,
                isTeam: isTeamMode
            });
            localStorage.setItem('teaFrameworkScores', JSON.stringify(scores));
        }
        
        // Player Setup Functions
        function showIndividualSetup() {
            document.getElementById('individualSetup').style.display = 'block';
            document.getElementById('teamSetup').style.display = 'none';
            isTeamMode = false;
            document.getElementById('playerName').focus();
        }
        
        function showTeamSetup() {
            document.getElementById('teamSetup').style.display = 'block';
            document.getElementById('individualSetup').style.display = 'none';
            isTeamMode = true;
            updateTeamMembers();
        }
        
        function updateTeamMembers() {
            const teamSelect = document.getElementById('teamSelect');
            const teamMembersDiv = document.getElementById('teamMembers');
            
            if (teamSelect.value) {
                const members = teamData[teamSelect.value];
                teamMembersDiv.innerHTML = `
                    <strong>Team Members:</strong><br>
                    ${members.map(member => `• ${member}`).join('<br>')}
                `;
                teamMembersDiv.style.display = 'block';
            } else {
                teamMembersDiv.style.display = 'none';
            }
        }
        
        function setTeamPlayer() {
            const teamSelect = document.getElementById('teamSelect');
            const nameInput = document.getElementById('teamPlayerName');
            const name = nameInput.value.trim();
            const team = teamSelect.value;
            
            if (!team) {
                alert('Please select your team!');
                return;
            }
            
            if (!name) {
                alert('Please enter your name!');
                return;
            }
            
            currentPlayer = name;
            currentTeam = team;
            document.getElementById('currentPlayerName').textContent = `${name} (${team})`;
            document.getElementById('playerGreeting').style.display = 'block';
            document.getElementById('gamesGrid').style.display = 'grid';
            document.getElementById('teamSetup').style.display = 'none';
        }
        function setPlayerName() {
            const nameInput = document.getElementById('playerName');
            const name = nameInput.value.trim();
            
            if (!name) {
                alert('Please enter your name!');
                return;
            }
            
            currentPlayer = name;
            currentTeam = '';
            document.getElementById('currentPlayerName').textContent = name;
            document.getElementById('playerGreeting').style.display = 'block';
            document.getElementById('gamesGrid').style.display = 'grid';
            document.getElementById('individualSetup').style.display = 'none';
        }
        
        // Navigation
        function showScreen(screenId) {
            document.querySelectorAll('.screen').forEach(screen => {
                screen.classList.remove('active');
            });
            document.getElementById(screenId).classList.add('active');
        }
        
        function goHome() {
            showScreen('homeScreen');
            resetGameState();
            
            // Reset headers back to default
            const termsHeader = document.querySelector('.matching-container .terms-column h3');
            const defsHeader = document.querySelector('.matching-container .definitions-column h3');
            if (termsHeader) termsHeader.textContent = 'Terms';
            if (defsHeader) defsHeader.textContent = 'Definitions';
            
            // Show the final score section when coming from a completed game
            const finalScoreDiv = document.querySelector('.final-score');
            if (finalScoreDiv) {
                finalScoreDiv.style.display = 'block';
            }
        }
        
        function resetGameState() {
            gameState = {
                selectedTerm: null,
                selectedDefinition: null,
                matches: new Map(),
                score: 0,
                currentGame: null,
                timeLeft: 60,
                quickMatchIndex: 0,
                attempts: new Map(),
                maxAttempts: 2
            };
        }
        
        // Start Games
        function startGame(gameType) {
            if (!currentPlayer) {
                alert('Please enter your name first!');
                return;
            }
            
            resetGameState();
            gameState.currentGame = gameType;
            
            switch(gameType) {
                case 'matching':
                    startMatchingGame();
                    break;
                case 'sorting':
                    startSortingGame();
                    break;
                case 'frameworkQuestions':
                    startFrameworkQuestionsGame();
                    break;
            }
        }
        
        // Matching Game
        function startMatchingGame() {
            showScreen('matchingScreen');
            document.getElementById('matchingPlayerName').textContent = currentPlayer;
            document.getElementById('matchingScore').textContent = '0';
            
            const terms = [...gameData.matching];
            shuffleArray(terms);
            
            const termsContainer = document.getElementById('termsContainer');
            const definitionsContainer = document.getElementById('definitionsContainer');
            
            termsContainer.innerHTML = '';
            definitionsContainer.innerHTML = '';
            
            // Create shuffled definitions
            const definitions = [...terms];
            shuffleArray(definitions);
            
            terms.forEach((item, index) => {
                const termElement = document.createElement('div');
                termElement.className = 'match-item';
                termElement.textContent = item.term;
                termElement.dataset.term = item.term;
                termElement.onclick = () => selectTerm(termElement);
                termsContainer.appendChild(termElement);
            });
            
            definitions.forEach((item, index) => {
                const defElement = document.createElement('div');
                defElement.className = 'match-item';
                defElement.textContent = item.definition;
                defElement.dataset.term = item.term;
                defElement.onclick = () => selectDefinition(defElement);
                definitionsContainer.appendChild(defElement);
            });
        }
        
        function selectTerm(element) {
            document.querySelectorAll('.terms-column .match-item').forEach(item => {
                item.classList.remove('selected');
            });
            element.classList.add('selected');
            gameState.selectedTerm = element.dataset.term;
            checkForMatch();
        }
        
        function selectDefinition(element) {
            document.querySelectorAll('.definitions-column .match-item').forEach(item => {
                item.classList.remove('selected');
            });
            element.classList.add('selected');
            gameState.selectedDefinition = element.dataset.term;
            checkForMatch();
        }
        
        function checkForMatch() {
            if (gameState.selectedTerm && gameState.selectedDefinition) {
                const termElement = document.querySelector(`[data-term="${gameState.selectedTerm}"]`);
                const defElement = document.querySelector(`.definitions-column [data-term="${gameState.selectedDefinition}"]`);
                
                // Create unique key for this term-definition pair
                const attemptKey = `${gameState.selectedTerm}-${gameState.selectedDefinition}`;
                
                if (gameState.selectedTerm === gameState.selectedDefinition) {
                    // Correct match
                    termElement.classList.remove('selected');
                    termElement.classList.add('correct');
                    defElement.classList.remove('selected');
                    defElement.classList.add('correct');
                    
                    gameState.matches.set(gameState.selectedTerm, gameState.selectedDefinition);
                    gameState.score++;
                    
                    termElement.onclick = null;
                    defElement.onclick = null;
                } else {
                    // Incorrect match - track attempts
                    const currentAttempts = gameState.attempts.get(attemptKey) || 0;
                    gameState.attempts.set(attemptKey, currentAttempts + 1);
                    
                    termElement.classList.add('incorrect');
                    defElement.classList.add('incorrect');
                    
                    if (currentAttempts + 1 >= gameState.maxAttempts) {
                        // Max attempts reached - disable these items
                        setTimeout(() => {
                            termElement.classList.remove('incorrect', 'selected');
                            defElement.classList.remove('incorrect', 'selected');
                            termElement.classList.add('disabled');
                            defElement.classList.add('disabled');
                            termElement.onclick = null;
                            defElement.onclick = null;
                            termElement.style.opacity = '0.5';
                            defElement.style.opacity = '0.5';
                        }, 1000);
                    } else {
                        setTimeout(() => {
                            termElement.classList.remove('incorrect', 'selected');
                            defElement.classList.remove('incorrect', 'selected');
                        }, 1000);
                    }
                }
                
                gameState.selectedTerm = null;
                gameState.selectedDefinition = null;
                updateMatchingProgress();
            }
        }
        
        function updateMatchingProgress() {
            const totalQuestions = gameState.currentGame === 'frameworkQuestions' ? 
                gameData.frameworkQuestions.length : gameData.matching.length;
            
            const progress = (gameState.score / totalQuestions) * 100;
            document.getElementById('matchingProgress').style.width = progress + '%';
            document.getElementById('matchingScore').textContent = gameState.score;
            
            if (gameState.score === totalQuestions) {
                setTimeout(() => {
                    finishGame(gameState.currentGame, gameState.score, totalQuestions);
                }, 1000);
            }
            
            // Enable submit button when at least one match is made
            document.getElementById('submitMatching').disabled = gameState.score === 0;
        }
        
        function submitMatching() {
            const totalQuestions = gameState.currentGame === 'frameworkQuestions' ? 
                gameData.frameworkQuestions.length : gameData.matching.length;
            finishGame(gameState.currentGame, gameState.score, totalQuestions);
        }
        
        // Sorting Game
        function startSortingGame() {
            showScreen('sortingScreen');
            document.getElementById('sortingPlayerName').textContent = currentPlayer;
            document.getElementById('sortingScore').textContent = '0';
            
            const items = [...gameData.sorting];
            shuffleArray(items);
            
            const container = document.getElementById('sortableItems');
            container.innerHTML = '';
            
            items.forEach(item => {
                const element = document.createElement('div');
                element.className = 'sortable-item';
                element.textContent = item.term;
                element.draggable = true;
                element.dataset.category = item.category;
                element.dataset.term = item.term;
                
                element.addEventListener('dragstart', handleDragStart);
                element.addEventListener('dragend', handleDragEnd);
                
                container.appendChild(element);
            });
            
            setupDropZones();
        }
        
        function setupDropZones() {
            document.querySelectorAll('.category-box').forEach(box => {
                box.addEventListener('dragover', handleDragOver);
                box.addEventListener('drop', handleDrop);
                box.addEventListener('dragenter', handleDragEnter);
                box.addEventListener('dragleave', handleDragLeave);
            });
        }
        
        function handleDragStart(e) {
            e.target.classList.add('dragging');
            e.dataTransfer.setData('text/plain', e.target.dataset.term);
        }
        
        function handleDragEnd(e) {
            e.target.classList.remove('dragging');
        }
        
        function handleDragOver(e) {
            e.preventDefault();
        }
        
        function handleDragEnter(e) {
            e.target.closest('.category-box').classList.add('drag-over');
        }
        
        function handleDragLeave(e) {
            if (!e.target.closest('.category-box').contains(e.relatedTarget)) {
                e.target.closest('.category-box').classList.remove('drag-over');
            }
        }
        
        function handleDrop(e) {
            e.preventDefault();
            const box = e.target.closest('.category-box');
            box.classList.remove('drag-over');
            
            const termData = e.dataTransfer.getData('text/plain');
            const draggedElement = document.querySelector(`[data-term="${termData}"]`);
            
            if (draggedElement && box) {
                const dropZone = box.querySelector('.drop-zone');
                dropZone.appendChild(draggedElement);
                draggedElement.classList.remove('dragging');
            }
        }
        
        function submitSorting() {
            let correct = 0;
            const total = gameData.sorting.length;
            
            document.querySelectorAll('.category-box').forEach(box => {
                const category = box.dataset.category;
                const items = box.querySelectorAll('.sortable-item');
                
                items.forEach(item => {
                    if (item.dataset.category === category) {
                        correct++;
                        item.style.background = '#d5f4e6';
                        item.style.borderColor = '#27ae60';
                    } else {
                        item.style.background = '#fdeaea';
                        item.style.borderColor = '#e74c3c';
                    }
                });
            });
            
            setTimeout(() => {
                finishGame('sorting', correct, total);
            }, 2000);
        }
        
        // Framework Questions Game
        function startFrameworkQuestionsGame() {
            showScreen('matchingScreen');
            document.getElementById('matchingPlayerName').textContent = currentPlayer;
            document.getElementById('matchingScore').textContent = '0';
            
            // Change headers for questions game
            document.querySelector('.matching-container .terms-column h3').textContent = 'Essential Questions';
            document.querySelector('.matching-container .definitions-column h3').textContent = 'Framework Areas';
            
            const questions = [...gameData.frameworkQuestions];
            shuffleArray(questions);
            
            const termsContainer = document.getElementById('termsContainer');
            const definitionsContainer = document.getElementById('definitionsContainer');
            
            termsContainer.innerHTML = '';
            definitionsContainer.innerHTML = '';
            
            // Create shuffled areas
            const areas = [...questions];
            shuffleArray(areas);
            
            questions.forEach((item, index) => {
                const questionElement = document.createElement('div');
                questionElement.className = 'match-item';
                questionElement.textContent = item.question;
                questionElement.dataset.term = item.question;
                questionElement.onclick = () => selectTerm(questionElement);
                questionElement.style.fontSize = '0.9em';
                questionElement.style.lineHeight = '1.4';
                termsContainer.appendChild(questionElement);
            });
            
            areas.forEach((item, index) => {
                const areaElement = document.createElement('div');
                areaElement.className = 'match-item';
                areaElement.textContent = item.area;
                areaElement.dataset.term = item.question;
                areaElement.onclick = () => selectDefinition(areaElement);
                areaElement.style.fontSize = '0.95em';
                areaElement.style.lineHeight = '1.4';
                definitionsContainer.appendChild(areaElement);
            });
            
            // Update progress tracking for framework questions
            gameState.currentGame = 'frameworkQuestions';
        }
        function startQuickMatchGame() {
            showScreen('quickMatchScreen');
            document.getElementById('quickMatchPlayerName').textContent = currentPlayer;
            document.getElementById('quickMatchScore').textContent = '0';
            document.getElementById('timeLeft').textContent = '60';
            
            gameState.timeLeft = 60;
            gameState.score = 0;
            gameState.quickMatchIndex = 0;
            
            startTimer();
            showNextQuickMatch();
        }
        
        function startTimer() {
            const timer = setInterval(() => {
                gameState.timeLeft--;
                document.getElementById('timeLeft').textContent = gameState.timeLeft;
                
                if (gameState.timeLeft <= 0) {
                    clearInterval(timer);
                    finishGame('quickMatch', gameState.score, gameState.quickMatchIndex);
                }
            }, 1000);
        }
        
        function showNextQuickMatch() {
            if (gameState.quickMatchIndex >= gameData.matching.length) {
                gameState.quickMatchIndex = 0; // Loop back to start
            }
            
            const currentItem = gameData.matching[gameState.quickMatchIndex];
            const incorrectItems = gameData.matching.filter(item => item.term !== currentItem.term);
            shuffleArray(incorrectItems);
            
            const options = [currentItem, ...incorrectItems.slice(0, 2)];
            shuffleArray(options);
            
            document.getElementById('quickTermContainer').innerHTML = `
                <div class="match-item" style="font-size: 1.2em; font-weight: bold;">
                    ${currentItem.term}
                </div>
            `;
            
            const container = document.getElementById('quickDefinitionsContainer');
            container.innerHTML = '';
            
            options.forEach(option => {
                const element = document.createElement('div');
                element.className = 'match-item';
                element.textContent = option.definition;
                element.onclick = () => selectQuickMatch(option.term === currentItem.term);
                container.appendChild(element);
            });
        }
        
        function selectQuickMatch(isCorrect) {
            gameState.quickMatchIndex++;
            
            if (isCorrect) {
                gameState.score++;
                document.getElementById('quickMatchScore').textContent = gameState.score;
            }
            
            if (gameState.timeLeft > 0) {
                setTimeout(showNextQuickMatch, 500);
            }
        }
        
        // Results and Leaderboard
        function finishGame(gameType, score, total) {
            const percentage = Math.round((score / total) * 100);
            
            document.getElementById('finalScore').textContent = percentage;
            document.getElementById('gameType').textContent = gameType.charAt(0).toUpperCase() + gameType.slice(1);
            
            saveScore(currentPlayer, gameType, score, total);
            updateLeaderboard();
            showAnswers();
            showScreen('resultsScreen');
        }
        
        function updateLeaderboard() {
            const scores = getScores();
            scores.sort((a, b) => b.score - a.score);
            
            const container = document.getElementById('leaderboardContainer');
            container.innerHTML = '';
            
            // Separate individual and team scores
            const individualScores = scores.filter(score => !score.isTeam);
            const teamScores = scores.filter(score => score.isTeam);
            
            // Show team leaderboard if there are team scores
            if (teamScores.length > 0) {
                const teamHeader = document.createElement('h4');
                teamHeader.textContent = '👥 Team Scores';
                teamHeader.style.color = '#2c3e50';
                teamHeader.style.marginBottom = '15px';
                container.appendChild(teamHeader);
                
                teamScores.slice(0, 10).forEach((score, index) => {
                    const item = document.createElement('div');
                    item.className = `leaderboard-item ${index === 0 ? 'top-score' : ''}`;
                    item.innerHTML = `
                        <span class="rank">#${index + 1}</span>
                        <span class="player-name">${score.player}</span>
                        <span style="font-size: 0.9em; color: #666;">${score.game}</span>
                        <span class="player-score">${score.score}%</span>
                    `;
                    container.appendChild(item);
                });
            }
            
            // Show individual leaderboard if there are individual scores
            if (individualScores.length > 0) {
                const individualHeader = document.createElement('h4');
                individualHeader.textContent = '👤 Individual Scores';
                individualHeader.style.color = '#2c3e50';
                individualHeader.style.marginTop = teamScores.length > 0 ? '30px' : '0';
                individualHeader.style.marginBottom = '15px';
                container.appendChild(individualHeader);
                
                individualScores.slice(0, 10).forEach((score, index) => {
                    const item = document.createElement('div');
                    item.className = `leaderboard-item ${index === 0 ? 'top-score' : ''}`;
                    item.innerHTML = `
                        <span class="rank">#${index + 1}</span>
                        <span class="player-name">${score.player}</span>
                        <span style="font-size: 0.9em; color: #666;">${score.game}</span>
                        <span class="player-score">${score.score}%</span>
                    `;
                    container.appendChild(item);
                });
            }
            
            // If no scores yet
            if (scores.length === 0) {
                container.innerHTML = '<p style="text-align: center; color: #666;">No scores yet. Play a game to get started!</p>';
            }
        }
        
        function showAnswers() {
            const container = document.getElementById('answersContainer');
            container.innerHTML = '';
            
            if (gameState.currentGame === 'sorting') {
                const categories = {
                    training: 'Quality of Candidate Training',
                    practice: 'Quality of Practice',
                    support: 'Quality of Candidate Support'
                };
                
                Object.keys(categories).forEach(cat => {
                    const categoryItems = gameData.sorting.filter(item => item.category === cat);
                    if (categoryItems.length > 0) {
                        const categoryHeader = document.createElement('h4');
                        categoryHeader.textContent = categories[cat];
                        categoryHeader.style.marginTop = '20px';
                        categoryHeader.style.color = '#2c3e50';
                        container.appendChild(categoryHeader);
                        
                        categoryItems.forEach(item => {
                            const answerItem = document.createElement('div');
                            answerItem.className = 'answer-item';
                            answerItem.innerHTML = `
                                <div class="answer-term">${item.term}</div>
                            `;
                            container.appendChild(answerItem);
                        });
                    }
                });
            } else if (gameState.currentGame === 'frameworkQuestions') {
                gameData.frameworkQuestions.forEach(item => {
                    const answerItem = document.createElement('div');
                    answerItem.className = 'answer-item';
                    answerItem.innerHTML = `
                        <div class="answer-term">${item.area}</div>
                        <div class="answer-definition">${item.question}</div>
                    `;
                    container.appendChild(answerItem);
                });
            } else {
                gameData.matching.forEach(item => {
                    const answerItem = document.createElement('div');
                    answerItem.className = 'answer-item';
                    answerItem.innerHTML = `
                        <div class="answer-term">${item.term}</div>
                        <div class="answer-definition">${item.definition}</div>
                    `;
                    container.appendChild(answerItem);
                });
            }
        }
        
        function showLeaderboard() {
            updateLeaderboard();
            showAnswers();
            showScreen('resultsScreen');
            
            // Hide the final score section when viewing leaderboard from home
            const finalScoreDiv = document.querySelector('.final-score');
            if (finalScoreDiv) {
                finalScoreDiv.style.display = 'none';
            }
        }
        
        function saveResults() {
            alert('Your score has been saved! You can view all scores on the leaderboard.');
        }
        
        // Utility Functions
        function shuffleArray(array) {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]];
            }
        }
        
        // Initialize
        document.addEventListener('DOMContentLoaded', function() {
            // Add team selection change listener
            const teamSelect = document.getElementById('teamSelect');
            if (teamSelect) {
                teamSelect.addEventListener('change', updateTeamMembers);
            }
            
            // Enter key handlers
            const playerNameInput = document.getElementById('playerName');
            if (playerNameInput) {
                playerNameInput.addEventListener('keypress', function(e) {
                    if (e.key === 'Enter') {
                        setPlayerName();
                    }
                });
            }
            
            const teamPlayerNameInput = document.getElementById('teamPlayerName');
            if (teamPlayerNameInput) {
                teamPlayerNameInput.addEventListener('keypress', function(e) {
                    if (e.key === 'Enter') {
                        setTeamPlayer();
                    }
                });
            }
        });
    </script>
</body>
</html>
