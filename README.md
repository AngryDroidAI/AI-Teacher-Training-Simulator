<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AI Teacher Training Simulator</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary: #4361ee;
            --secondary: #3a0ca3;
            --accent: #f72585;
            --success: #4cc9f0;
            --warning: #f8961e;
            --danger: #e63946;
            --light: #f8f9fa;
            --dark: #212529;
            --gray: #6c757d;
            --light-gray: #e9ecef;
            --border-radius: 12px;
            --box-shadow: 0 4px 20px rgba(0, 0, 0, 0.08);
            --transition: all 0.3s ease;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
            min-height: 100vh;
            color: var(--dark);
            padding: 20px;
        }

        .dashboard {
            display: grid;
            grid-template-columns: 250px 1fr;
            grid-template-rows: auto 1fr;
            grid-template-areas:
                "header header"
                "sidebar main";
            gap: 20px;
            max-width: 1600px;
            margin: 0 auto;
        }

        /* HEADER */
        .header {
            grid-area: header;
            background: white;
            border-radius: var(--border-radius);
            padding: 20px 30px;
            box-shadow: var(--box-shadow);
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .logo {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .logo-icon {
            font-size: 2.2rem;
            color: var(--primary);
        }

        .logo-text h1 {
            font-size: 1.8rem;
            color: var(--primary);
        }

        .logo-text p {
            font-size: 0.9rem;
            color: var(--gray);
        }

        .user-info {
            display: flex;
            align-items: center;
            gap: 20px;
        }

        .user-avatar {
            width: 45px;
            height: 45px;
            border-radius: 50%;
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-weight: bold;
            font-size: 1.2rem;
        }

        /* SIDEBAR */
        .sidebar {
            grid-area: sidebar;
            background: white;
            border-radius: var(--border-radius);
            padding: 25px 0;
            box-shadow: var(--box-shadow);
            display: flex;
            flex-direction: column;
        }

        .nav-section {
            padding: 0 20px;
            margin-bottom: 30px;
        }

        .nav-title {
            font-size: 0.85rem;
            text-transform: uppercase;
            color: var(--gray);
            margin-bottom: 15px;
            font-weight: 600;
            letter-spacing: 1px;
        }

        .nav-item {
            display: flex;
            align-items: center;
            gap: 12px;
            padding: 14px 15px;
            margin-bottom: 8px;
            border-radius: 10px;
            cursor: pointer;
            transition: var(--transition);
            color: var(--dark);
            text-decoration: none;
        }

        .nav-item:hover {
            background-color: var(--light-gray);
        }

        .nav-item.active {
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            color: white;
            box-shadow: 0 4px 12px rgba(67, 97, 238, 0.3);
        }

        .nav-icon {
            font-size: 1.2rem;
        }

        .progress-section {
            padding: 20px;
            margin-top: auto;
            background: linear-gradient(135deg, #f8f9fa, #e9ecef);
            border-radius: 0 0 var(--border-radius) var(--border-radius);
        }

        .progress-title {
            font-size: 1rem;
            margin-bottom: 15px;
            color: var(--dark);
        }

        .progress-bar {
            height: 8px;
            background-color: var(--light-gray);
            border-radius: 4px;
            overflow: hidden;
            margin-bottom: 10px;
        }

        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, var(--success), #2a9d8f);
            width: 65%;
            border-radius: 4px;
        }

        .progress-text {
            font-size: 0.9rem;
            color: var(--gray);
            display: flex;
            justify-content: space-between;
        }

        /* MAIN CONTENT */
        .main-content {
            grid-area: main;
            display: grid;
            grid-template-columns: repeat(12, 1fr);
            grid-auto-rows: minmax(150px, auto);
            gap: 20px;
        }

        .card {
            background: white;
            border-radius: var(--border-radius);
            padding: 25px;
            box-shadow: var(--box-shadow);
            transition: var(--transition);
        }

        .card:hover {
            transform: translateY(-5px);
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.12);
        }

        .card-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }

        .card-title {
            font-size: 1.3rem;
            color: var(--dark);
            font-weight: 600;
        }

        .card-icon {
            font-size: 1.8rem;
            color: var(--primary);
        }

        /* STATS CARDS */
        .stat-card {
            grid-column: span 3;
            display: flex;
            flex-direction: column;
        }

        .stat-value {
            font-size: 2.5rem;
            font-weight: 700;
            color: var(--primary);
            margin-bottom: 5px;
        }

        .stat-label {
            font-size: 1rem;
            color: var(--gray);
        }

        .stat-change {
            margin-top: auto;
            font-size: 0.9rem;
            display: flex;
            align-items: center;
            gap: 5px;
        }

        .stat-change.positive {
            color: #2a9d8f;
        }

        .stat-change.negative {
            color: var(--danger);
        }

        /* SCENARIO CARDS */
        .scenario-card {
            grid-column: span 4;
            display: flex;
            flex-direction: column;
        }

        .scenario-difficulty {
            display: inline-block;
            padding: 5px 12px;
            border-radius: 20px;
            font-size: 0.8rem;
            font-weight: 600;
            margin-bottom: 15px;
            align-self: flex-start;
        }

        .difficulty-beginner {
            background-color: rgba(76, 201, 240, 0.15);
            color: #1d6fa5;
        }

        .difficulty-intermediate {
            background-color: rgba(248, 150, 30, 0.15);
            color: #c56d00;
        }

        .difficulty-advanced {
            background-color: rgba(231, 57, 70, 0.15);
            color: #a81c2a;
        }

        .scenario-description {
            color: var(--gray);
            margin-bottom: 20px;
            line-height: 1.5;
            flex-grow: 1;
        }

        .scenario-footer {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-top: auto;
        }

        .scenario-time {
            font-size: 0.9rem;
            color: var(--gray);
            display: flex;
            align-items: center;
            gap: 5px;
        }

        .btn {
            padding: 10px 20px;
            border-radius: 8px;
            border: none;
            font-weight: 600;
            cursor: pointer;
            transition: var(--transition);
            display: inline-flex;
            align-items: center;
            gap: 8px;
        }

        .btn-primary {
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            color: white;
        }

        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 15px rgba(67, 97, 238, 0.3);
        }

        .btn-outline {
            background: transparent;
            color: var(--primary);
            border: 2px solid var(--primary);
        }

        .btn-outline:hover {
            background-color: rgba(67, 97, 238, 0.05);
        }

        /* METRICS CHART */
        .metrics-card {
            grid-column: span 6;
            grid-row: span 2;
        }

        .metrics-chart {
            height: 300px;
            display: flex;
            align-items: flex-end;
            gap: 30px;
            margin-top: 20px;
            padding: 20px 0;
        }

        .metric-bar {
            flex: 1;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        .bar {
            width: 40px;
            border-radius: 8px 8px 0 0;
            transition: var(--transition);
        }

        .bar:hover {
            opacity: 0.9;
            transform: scale(1.05);
        }

        .bar-label {
            margin-top: 10px;
            font-size: 0.9rem;
            color: var(--gray);
        }

        /* AI TOOLS */
        .tools-card {
            grid-column: span 6;
        }

        .tools-list {
            display: flex;
            flex-direction: column;
            gap: 15px;
        }

        .tool-item {
            display: flex;
            align-items: center;
            padding: 15px;
            border-radius: 10px;
            background-color: var(--light-gray);
            transition: var(--transition);
        }

        .tool-item:hover {
            background-color: #e2e6ea;
        }

        .tool-icon {
            width: 50px;
            height: 50px;
            border-radius: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.5rem;
            color: white;
            margin-right: 15px;
        }

        .tool-info {
            flex-grow: 1;
        }

        .tool-name {
            font-weight: 600;
            margin-bottom: 5px;
        }

        .tool-category {
            font-size: 0.85rem;
            color: var(--gray);
        }

        .tool-status {
            font-size: 0.8rem;
            padding: 4px 10px;
            border-radius: 20px;
            font-weight: 600;
        }

        .status-active {
            background-color: rgba(76, 201, 240, 0.15);
            color: #1d6fa5;
        }

        .status-inactive {
            background-color: rgba(108, 117, 125, 0.15);
            color: var(--gray);
        }

        /* SIMULATION CONSOLE */
        .console-card {
            grid-column: span 12;
            grid-row: span 2;
        }

        .console-output {
            background-color: #1e1e1e;
            color: #d4d4d4;
            height: 250px;
            border-radius: 8px;
            padding: 20px;
            font-family: 'Courier New', monospace;
            font-size: 0.95rem;
            overflow-y: auto;
            margin-bottom: 20px;
        }

        .console-input {
            display: flex;
            gap: 10px;
        }

        .console-input input {
            flex-grow: 1;
            padding: 12px 15px;
            border-radius: 8px;
            border: 2px solid var(--light-gray);
            font-size: 1rem;
        }

        .console-input input:focus {
            outline: none;
            border-color: var(--primary);
        }

        /* RESPONSIVE DESIGN */
        @media (max-width: 1200px) {
            .dashboard {
                grid-template-columns: 1fr;
                grid-template-areas:
                    "header"
                    "main";
            }
            
            .sidebar {
                display: none;
            }
            
            .stat-card, .scenario-card {
                grid-column: span 6;
            }
            
            .metrics-card, .tools-card {
                grid-column: span 12;
            }
        }

        @media (max-width: 768px) {
            .stat-card, .scenario-card {
                grid-column: span 12;
            }
            
            .header {
                flex-direction: column;
                gap: 20px;
                text-align: center;
            }
            
            .user-info {
                flex-direction: column;
                gap: 10px;
            }
        }
    </style>
</head>
<body>
    <div class="dashboard">
        <!-- HEADER -->
        <header class="header">
            <div class="logo">
                <div class="logo-icon">
                    <i class="fas fa-robot"></i>
                </div>
                <div class="logo-text">
                    <h1>AI Teacher Training Simulator</h1>
                    <p>Practice AI Integration in Safe Virtual Classrooms</p>
                </div>
            </div>
            <div class="user-info">
                <div class="user-avatar">TJ</div>
                <div>
                    <h3>Teacher Jordan</h3>
                    <p>Grade 8 Science • Level 2 Trainer</p>
                </div>
            </div>
        </header>

        <!-- SIDEBAR -->
        <nav class="sidebar">
            <div class="nav-section">
                <div class="nav-title">Training Modules</div>
                <a href="#" class="nav-item active">
                    <i class="fas fa-home nav-icon"></i>
                    <span>Dashboard</span>
                </a>
                <a href="#" class="nav-item">
                    <i class="fas fa-graduation-cap nav-icon"></i>
                    <span>AI Foundations</span>
                </a>
                <a href="#" class="nav-item">
                    <i class="fas fa-chalkboard-teacher nav-icon"></i>
                    <span>Classroom Integration</span>
                </a>
                <a href="#" class="nav-item">
                    <i class="fas fa-balance-scale nav-icon"></i>
                    <span>Ethical Challenges</span>
                </a>
                <a href="#" class="nav-item">
                    <i class="fas fa-chart-line nav-icon"></i>
                    <span>Data Analysis Lab</span>
                </a>
            </div>
            
            <div class="nav-section">
                <div class="nav-title">Simulation Tools</div>
                <a href="#" class="nav-item">
                    <i class="fas fa-vr-cardboard nav-icon"></i>
                    <span>Virtual Classroom</span>
                </a>
                <a href="#" class="nav-item">
                    <i class="fas fa-comments nav-icon"></i>
                    <span>Parent Communication</span>
                </a>
                <a href="#" class="nav-item">
                    <i class="fas fa-tools nav-icon"></i>
                    <span>AI Tool Sandbox</span>
                </a>
                <a href="#" class="nav-item">
                    <i class="fas fa-scroll nav-icon"></i>
                    <span>Policy Simulator</span>
                </a>
            </div>
            
            <div class="progress-section">
                <div class="progress-title">Training Progress</div>
                <div class="progress-bar">
                    <div class="progress-fill"></div>
                </div>
                <div class="progress-text">
                    <span>65% Complete</span>
                    <span>Level 2</span>
                </div>
            </div>
        </nav>

        <!-- MAIN CONTENT -->
        <main class="main-content">
            <!-- STATS CARDS -->
            <div class="card stat-card">
                <div class="card-header">
                    <div class="card-title">Simulations Completed</div>
                    <div class="card-icon">
                        <i class="fas fa-play-circle"></i>
                    </div>
                </div>
                <div class="stat-value">24</div>
                <div class="stat-label">Out of 40 Required</div>
                <div class="stat-change positive">
                    <i class="fas fa-arrow-up"></i>
                    <span>+3 this week</span>
                </div>
            </div>
            
            <div class="card stat-card">
                <div class="card-header">
                    <div class="card-title">Pedagogical Score</div>
                    <div class="card-icon">
                        <i class="fas fa-chart-bar"></i>
                    </div>
                </div>
                <div class="stat-value">88%</div>
                <div class="stat-label">Teaching Effectiveness</div>
                <div class="stat-change positive">
                    <i class="fas fa-arrow-up"></i>
                    <span>+5% this month</span>
                </div>
            </div>
            
            <div class="card stat-card">
                <div class="card-header">
                    <div class="card-title">Ethical Score</div>
                    <div class="card-icon">
                        <i class="fas fa-balance-scale"></i>
                    </div>
                </div>
                <div class="stat-value">92%</div>
                <div class="stat-label">Decision Alignment</div>
                <div class="stat-change positive">
                    <i class="fas fa-arrow-up"></i>
                    <span>+2% this month</span>
                </div>
            </div>
            
            <div class="card stat-card">
                <div class="card-header">
                    <div class="card-title">Time Saved</div>
                    <div class="card-icon">
                        <i class="fas fa-clock"></i>
                    </div>
                </div>
                <div class="stat-value">14.5h</div>
                <div class="stat-label">Administrative Tasks</div>
                <div class="stat-change positive">
                    <i class="fas fa-arrow-up"></i>
                    <span>+2h this week</span>
                </div>
            </div>

            <!-- SCENARIO CARDS -->
            <div class="card scenario-card">
                <div class="card-header">
                    <div class="card-title">Biased AI Grading</div>
                    <div class="scenario-difficulty difficulty-intermediate">Intermediate</div>
                </div>
                <p class="scenario-description">
                    An AI grading tool consistently gives lower scores to essays from ESL students. How do you address this bias while maintaining efficiency?
                </p>
                <div class="scenario-footer">
                    <div class="scenario-time">
                        <i class="far fa-clock"></i>
                        <span>15-20 min</span>
                    </div>
                    <button class="btn btn-primary" onclick="startSimulation(1)">
                        <i class="fas fa-play"></i>
                        Start Simulation
                    </button>
                </div>
            </div>
            
            <div class="card scenario-card">
                <div class="card-header">
                    <div class="card-title">Parent AI Concerns</div>
                    <div class="scenario-difficulty difficulty-beginner">Beginner</div>
                </div>
                <p class="scenario-description">
                    A parent is concerned that AI tools are replacing human interaction in your classroom. Practice your communication and reassurance strategies.
                </p>
                <div class="scenario-footer">
                    <div class="scenario-time">
                        <i class="far fa-clock"></i>
                        <span>10-15 min</span>
                    </div>
                    <button class="btn btn-primary" onclick="startSimulation(2)">
                        <i class="fas fa-play"></i>
                        Start Simulation
                    </button>
                </div>
            </div>
            
            <div class="card scenario-card">
                <div class="card-header">
                    <div class="card-title">Tech Failure Response</div>
                    <div class="scenario-difficulty difficulty-advanced">Advanced</div>
                </div>
                <p class="scenario-description">
                    The school's internet goes down during an AI-dependent lesson. How do you adapt your teaching without technology while maintaining learning objectives?
                </p>
                <div class="scenario-footer">
                    <div class="scenario-time">
                        <i class="far fa-clock"></i>
                        <span>20-25 min</span>
                    </div>
                    <button class="btn btn-primary" onclick="startSimulation(3)">
                        <i class="fas fa-play"></i>
                        Start Simulation
                    </button>
                </div>
            </div>

            <!-- METRICS CHART -->
            <div class="card metrics-card">
                <div class="card-header">
                    <div class="card-title">AI Integration Performance Metrics</div>
                    <button class="btn btn-outline">
                        <i class="fas fa-download"></i>
                        Export Data
                    </button>
                </div>
                <div class="metrics-chart" id="metricsChart">
                    <!-- Chart bars will be generated by JavaScript -->
                </div>
            </div>

            <!-- AI TOOLS -->
            <div class="card tools-card">
                <div class="card-header">
                    <div class="card-title">Available AI Tools</div>
                    <button class="btn btn-outline">
                        <i class="fas fa-plus"></i>
                        Add Tool
                    </button>
                </div>
                <div class="tools-list">
                    <div class="tool-item">
                        <div class="tool-icon" style="background: linear-gradient(135deg, #4361ee, #3a0ca3);">
                            <i class="fas fa-robot"></i>
                        </div>
                        <div class="tool-info">
                            <div class="tool-name">Adaptive Learning Platform</div>
                            <div class="tool-category">Personalized Instruction</div>
                        </div>
                        <div class="tool-status status-active">Active</div>
                    </div>
                    
                    <div class="tool-item">
                        <div class="tool-icon" style="background: linear-gradient(135deg, #f72585, #b5179e);">
                            <i class="fas fa-spell-check"></i>
                        </div>
                        <div class="tool-info">
                            <div class="tool-name">AI Writing Assistant</div>
                            <div class="tool-category">Feedback & Assessment</div>
                        </div>
                        <div class="tool-status status-active">Active</div>
                    </div>
                    
                    <div class="tool-item">
                        <div class="tool-icon" style="background: linear-gradient(135deg, #4cc9f0, #4895ef);">
                            <i class="fas fa-chart-pie"></i>
                        </div>
                        <div class="tool-info">
                            <div class="tool-name">Learning Analytics Dashboard</div>
                            <div class="tool-category">Data Analysis</div>
                        </div>
                        <div class="tool-status status-inactive">Needs Setup</div>
                    </div>
                </div>
            </div>

            <!-- SIMULATION CONSOLE -->
            <div class="card console-card">
                <div class="card-header">
                    <div class="card-title">AI Simulation Console</div>
                    <div>
                        <button class="btn btn-outline" onclick="clearConsole()">
                            <i class="fas fa-trash-alt"></i>
                            Clear
                        </button>
                        <button class="btn btn-primary" onclick="runAIAnalysis()">
                            <i class="fas fa-cogs"></i>
                            Run AI Analysis
                        </button>
                    </div>
                </div>
                <div class="console-output" id="consoleOutput">
                    <div>> Welcome to AI Teacher Training Simulator v2.1</div>
                    <div>> System initialized. Ready for simulation.</div>
                    <div>> Last simulation: "Biased AI Grading" completed at 10:30 AM</div>
                    <div>> Pedagogical Score: 88% | Ethical Score: 92%</div>
                    <div>> Recommendation: Try "Tech Failure Response" scenario next.</div>
                    <div>> Type 'help' for available commands.</div>
                </div>
                <div class="console-input">
                    <input type="text" id="consoleInput" placeholder="Enter simulation command or ask AI for advice..." onkeypress="handleConsoleInput(event)">
                    <button class="btn btn-primary" onclick="processConsoleCommand()">
                        <i class="fas fa-paper-plane"></i>
                        Send
                    </button>
                </div>
            </div>
        </main>
    </div>

    <script>
        // Initialize metrics chart
        function initMetricsChart() {
            const metrics = [
                { label: 'Pedagogical', value: 88, color: '#4361ee' },
                { label: 'Ethical', value: 92, color: '#4cc9f0' },
                { label: 'Efficiency', value: 76, color: '#f72585' },
                { label: 'Adaptability', value: 81, color: '#f8961e' },
                { label: 'Tech Literacy', value: 95, color: '#2a9d8f' },
                { label: 'Communication', value: 85, color: '#7209b7' }
            ];
            
            const chartContainer = document.getElementById('metricsChart');
            chartContainer.innerHTML = '';
            
            metrics.forEach(metric => {
                const barContainer = document.createElement('div');
                barContainer.className = 'metric-bar';
                
                const bar = document.createElement('div');
                bar.className = 'bar';
                bar.style.height = `${metric.value}%`;
                bar.style.backgroundColor = metric.color;
                bar.title = `${metric.label}: ${metric.value}%`;
                
                const label = document.createElement('div');
                label.className = 'bar-label';
                label.textContent = metric.label;
                
                barContainer.appendChild(bar);
                barContainer.appendChild(label);
                chartContainer.appendChild(barContainer);
                
                // Add click event to bars
                bar.addEventListener('click', () => {
                    showMetricDetails(metric);
                });
            });
        }
        
        // Show metric details
        function showMetricDetails(metric) {
            const messages = [
                `Analyzing ${metric.label} metric...`,
                `Current score: ${metric.value}%`,
                metric.value >= 80 
                    ? `Great job! You're performing well in this area.`
                    : `Consider focusing on improving this skill.`,
                `Recommendation: ${getMetricRecommendation(metric.label)}`
            ];
            
            addToConsole(messages);
        }
        
        // Get recommendations based on metric
        function getMetricRecommendation(metricName) {
            const recommendations = {
                'Pedagogical': 'Try the "Mixed Ability Classroom" scenario.',
                'Ethical': 'Review the Ethics in AI Education module.',
                'Efficiency': 'Explore automation tools in the AI Tool Sandbox.',
                'Adaptability': 'Practice the "Tech Failure Response" scenario.',
                'Tech Literacy': 'Complete the AI Foundations course.',
                'Communication': 'Use the Parent Communication simulator.'
            };
            
            return recommendations[metricName] || 'Continue with your current training path.';
        }
        
        // Start simulation
        function startSimulation(id) {
            const scenarios = {
                1: {
                    name: "Biased AI Grading",
                    messages: [
                        "> Starting simulation: Biased AI Grading",
                        "> Scenario: You notice an AI grading tool gives consistently lower scores to ESL student essays.",
                        "> Available actions:",
                        "  1. Adjust AI parameters to reduce bias",
                        "  2. Manually review all ESL essays",
                        "  3. Use a different assessment tool",
                        "  4. Combine AI scoring with teacher review",
                        "> What would you like to do? (Type option number or ask for advice)"
                    ]
                },
                2: {
                    name: "Parent AI Concerns",
                    messages: [
                        "> Starting simulation: Parent AI Concerns",
                        "> Scenario: Mrs. Johnson is worried AI is replacing human interaction in your classroom.",
                        "> She says: 'I don't want a robot teaching my child!'",
                        "> Available responses:",
                        "  1. Explain how AI augments, not replaces, teaching",
                        "  2. Invite her to observe a class using AI tools",
                        "  3. Share research on AI's educational benefits",
                        "  4. Adjust your use of AI based on her concerns",
                        "> How would you respond? (Type option number or ask for advice)"
                    ]
                },
                3: {
                    name: "Tech Failure Response",
                    messages: [
                        "> Starting simulation: Tech Failure Response",
                        "> Scenario: School internet fails during an AI-dependent lesson.",
                        "> Students are frustrated. Lesson plan is disrupted.",
                        "> Available actions:",
                        "  1. Switch to offline backup activities",
                        "  2. Use mobile hotspot for critical functions",
                        "  3. Turn failure into teachable moment about tech reliance",
                        "  4. Rearrange lesson schedule entirely",
                        "> What would you do? (Type option number or ask for advice)"
                    ]
                }
            };
            
            const scenario = scenarios[id];
            if (scenario) {
                addToConsole([`> Loading simulation: ${scenario.name}...`]);
                
                // Clear console after a delay and load scenario
                setTimeout(() => {
                    clearConsole();
                    setTimeout(() => {
                        addToConsole(scenario.messages);
                    }, 300);
                }, 800);
                
                // Update stats
                updateStatsAfterSimulation();
            }
        }
        
        // Update stats after simulation
        function updateStatsAfterSimulation() {
            // Simulate stat increases
            const statValueElements = document.querySelectorAll('.stat-value');
            statValueElements.forEach(el => {
                const current = parseInt(el.textContent);
                if (!isNaN(current) && current < 100) {
                    // Small random increase
                    const increase = Math.floor(Math.random() * 3) + 1;
                    el.textContent = Math.min(current + increase, 100) + (el.textContent.includes('%') ? '%' : '');
                }
            });
            
            // Update progress bar
            const progressFill = document.querySelector('.progress-fill');
            const currentWidth = parseInt(progressFill.style.width) || 65;
            progressFill.style.width = Math.min(currentWidth + 2, 100) + '%';
            
            const progressText = document.querySelector('.progress-text span');
            const currentPercent = parseInt(progressText.textContent) || 65;
            progressText.textContent = Math.min(currentPercent + 2, 100) + '% Complete';
        }
        
        // Console functions
        function addToConsole(messages) {
            const consoleOutput = document.getElementById('consoleOutput');
            
            if (Array.isArray(messages)) {
                messages.forEach(msg => {
                    const div = document.createElement('div');
                    div.innerHTML = `> ${msg}`;
                    consoleOutput.appendChild(div);
                });
            } else {
                const div = document.createElement('div');
                div.innerHTML = `> ${messages}`;
                consoleOutput.appendChild(div);
            }
            
            // Scroll to bottom
            consoleOutput.scrollTop = consoleOutput.scrollHeight;
        }
        
        function clearConsole() {
            const consoleOutput = document.getElementById('consoleOutput');
            consoleOutput.innerHTML = '<div>> Console cleared. Ready for new simulation.</div>';
        }
        
        function handleConsoleInput(event) {
            if (event.key === 'Enter') {
                processConsoleCommand();
            }
        }
        
        function processConsoleCommand() {
            const input = document.getElementById('consoleInput');
            const command = input.value.trim();
            
            if (command) {
                addToConsole(`User: ${command}`);
                
                // Process command
                if (command.toLowerCase() === 'help') {
                    showHelp();
                } else if (command.toLowerCase() === 'stats') {
                    showStats();
                } else if (command.toLowerCase().includes('advice')) {
                    giveAdvice();
                } else if (command.match(/^\d+$/)) {
                    processScenarioChoice(parseInt(command));
                } else {
                    addToConsole("AI: I'm not sure how to respond to that. Type 'help' for available commands.");
                }
                
                input.value = '';
            }
        }
        
        function showHelp() {
            const helpMessages = [
                "Available commands:",
                "  'help' - Show this help message",
                "  'stats' - Show your training statistics",
                "  'advice' - Get personalized AI advice",
                "  '1', '2', '3', '4' - Choose scenario options",
                "  'simulation [number]' - Start a simulation",
                "  'tools' - List available AI tools",
                "  'reset' - Reset console"
            ];
            
            addToConsole(helpMessages);
        }
        
        function showStats() {
            const stats = [
                "Your current training statistics:",
                "  Simulations completed: 24/40",
                "  Pedagogical Score: 88%",
                "  Ethical Score: 92%",
                "  Efficiency Gain: 14.5 hours saved",
                "  Overall Progress: Level 2 (65%)",
                "  Next milestone: Level 3 at 75%"
            ];
            
            addToConsole(stats);
        }
        
        function giveAdvice() {
            const advice = [
                "AI Analysis: Based on your performance data...",
                "1. Your ethical decision-making is strong (92%).",
                "2. Consider practicing more tech failure scenarios.",
                "3. Try integrating the Learning Analytics Dashboard tool.",
                "4. Recommended next simulation: 'Tech Failure Response'.",
                "5. Join the Thursday webinar: 'AI & Special Education'"
            ];
            
            addToConsole(advice);
        }
        
        function processScenarioChoice(choice) {
            const responses = [
                "You chose option " + choice + ". Let's see what happens...",
                "The AI system processes your decision...",
                getScenarioOutcome(choice)
            ];
            
            addToConsole(responses);
        }
        
        function getScenarioOutcome(choice) {
            const outcomes = [
                "Outcome: This approach shows good technical understanding but may increase your workload.",
                "Outcome: This is a balanced approach that addresses both ethics and practicality.",
                "Outcome: This conservative choice minimizes risk but may not leverage AI's full potential.",
                "Outcome: This innovative approach could set a new standard for AI integration!"
            ];
            
            return outcomes[choice - 1] || "AI: That's not a valid choice for this scenario. Please try again.";
        }
        
        function runAIAnalysis() {
            addToConsole("Running comprehensive AI analysis of your training data...");
            
            setTimeout(() => {
                const analysis = [
                    "AI Analysis Complete:",
                    "1. You excel at ethical decision-making in AI contexts.",
                    "2. Your adaptability score has improved 12% this month.",
                    "3. Consider exploring more advanced AI tools in the sandbox.",
                    "4. Prediction: You'll reach Level 3 in approximately 2 weeks.",
                    "5. Recommendation: Share your experiences in the teacher forum."
                ];
                
                addToConsole(analysis);
            }, 1500);
        }
        
        // Initialize dashboard when page loads
        document.addEventListener('DOMContentLoaded', function() {
            initMetricsChart();
            
            // Set up navigation item clicks
            document.querySelectorAll('.nav-item').forEach(item => {
                item.addEventListener('click', function(e) {
                    e.preventDefault();
                    document.querySelectorAll('.nav-item').forEach(nav => nav.classList.remove('active'));
                    this.classList.add('active');
                    
                    const moduleName = this.querySelector('span').textContent;
                    addToConsole(`Switched to module: ${moduleName}`);
                });
            });
            
            // Set up tool item clicks
            document.querySelectorAll('.tool-item').forEach(item => {
                item.addEventListener('click', function() {
                    const toolName = this.querySelector('.tool-name').textContent;
                    addToConsole(`Selected tool: ${toolName}. Click 'Setup' to configure.`);
                });
            });
            
            // Welcome message
            setTimeout(() => {
                addToConsole("AI Assistant: Welcome back, Teacher Jordan! Ready for today's training?");
            }, 1000);
        });
    </script>
</body>
</html>
