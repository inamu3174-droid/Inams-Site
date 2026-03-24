<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CricketLive - Live Scores & Updates</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: #0f1419;
            color: #fff;
            line-height: 1.6;
        }

        /* Header */
        .header {
            background: linear-gradient(135deg, #1e3c72 0%, #2a5298 100%);
            padding: 1rem 0;
            position: sticky;
            top: 0;
            z-index: 1000;
            box-shadow: 0 2px 10px rgba(0,0,0,0.3);
        }

        .nav {
            max-width: 1200px;
            margin: 0 auto;
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 0 2rem;
        }

        .logo {
            font-size: 1.8rem;
            font-weight: bold;
            color: #fff;
        }

        .nav-links {
            display: flex;
            list-style: none;
            gap: 2rem;
        }

        .nav-links a {
            color: #fff;
            text-decoration: none;
            font-weight: 500;
            transition: color 0.3s;
        }

        .nav-links a:hover {
            color: #ffd700;
        }

        .search-box {
            display: flex;
            background: rgba(255,255,255,0.1);
            border-radius: 25px;
            padding: 0.5rem 1rem;
            width: 250px;
        }

        .search-box input {
            background: none;
            border: none;
            color: #fff;
            flex: 1;
            outline: none;
        }

        /* Main Container */
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 2rem;
        }

        /* Live Matches Section */
        .live-matches {
            margin-bottom: 2rem;
        }

        .section-title {
            font-size: 1.5rem;
            margin-bottom: 1rem;
            color: #ffd700;
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }

        .match-card {
            background: #1a1f2b;
            border-radius: 10px;
            padding: 1.5rem;
            margin-bottom: 1rem;
            border-left: 4px solid #ffd700;
            transition: transform 0.3s, box-shadow 0.3s;
        }

        .match-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 25px rgba(255,215,0,0.2);
        }

        .match-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1rem;
        }

        .match-status {
            background: #28a745;
            padding: 0.3rem 0.8rem;
            border-radius: 20px;
            font-size: 0.9rem;
            font-weight: bold;
        }

        .match-teams {
            display: flex;
            gap: 2rem;
            margin-bottom: 1rem;
        }

        .team {
            flex: 1;
            text-align: center;
        }

        .team-name {
            font-size: 1.1rem;
            font-weight: bold;
            margin-bottom: 0.5rem;
        }

        .team-score {
            font-size: 1.8rem;
            font-weight: bold;
            color: #ffd700;
        }

        .match-details {
            display: flex;
            gap: 1rem;
            font-size: 0.9rem;
            color: #ccc;
        }

        /* Fixtures & Results */
        .fixtures-results {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 2rem;
            margin-bottom: 2rem;
        }

        .section {
            background: #1a1f2b;
            padding: 1.5rem;
            border-radius: 10px;
        }

        .fixture-item, .result-item {
            padding: 1rem;
            border-bottom: 1px solid #333;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .fixture-item:last-child, .result-item:last-child {
            border-bottom: none;
        }

        /* News Section */
        .news-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 1.5rem;
            margin-top: 2rem;
        }

        .news-card {
            background: #1a1f2b;
            border-radius: 10px;
            overflow: hidden;
            transition: transform 0.3s;
        }

        .news-card:hover {
            transform: translateY(-5px);
        }

        .news-image {
            height: 200px;
            background: linear-gradient(45deg, #667eea 0%, #764ba2 100%);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 3rem;
            color: rgba(255,255,255,0.8);
        }

        .news-content {
            padding: 1.5rem;
        }

        .news-title {
            font-size: 1.1rem;
            margin-bottom: 0.5rem;
            color: #ffd700;
        }

        /* Responsive */
        @media (max-width: 768px) {
            .nav {
                flex-direction: column;
                gap: 1rem;
            }

            .nav-links {
                gap: 1rem;
            }

            .search-box {
                width: 100%;
            }

            .fixtures-results {
                grid-template-columns: 1fr;
            }

            .match-teams {
                flex-direction: column;
                gap: 1rem;
            }
        }

        /* Live Indicator Animation */
        @keyframes pulse {
            0% { opacity: 1; }
            50% { opacity: 0.5; }
            100% { opacity: 1; }
        }

        .live-indicator {
            animation: pulse 2s infinite;
        }
    </style>
</head>
<body>
    <!-- Header -->
    <header class="header">
        <nav class="nav">
            <div class="logo">
                <i class="fas fa-circle-notch"></i> CricketLive
            </div>
            <ul class="nav-links">
                <li><a href="#live">Live Scores</a></li>
                <li><a href="#schedule">Schedule</a></li>
                <li><a href="#rankings">Rankings</a></li>
                <li><a href="#news">News</a></li>
            </ul>
            <div class="search-box">
                <i class="fas fa-search"></i>
                <input type="text" placeholder="Search matches, teams...">
            </div>
        </nav>
    </header>

    <div class="container">
        <!-- Live Matches -->
        <section class="live-matches" id="live">
            <h2 class="section-title">
                <i class="fas fa-fire live-indicator"></i>
                Live Matches
            </h2>
            
            <div class="match-card">
                <div class="match-header">
                    <span>1st ODI • 2nd innings</span>
                    <span class="match-status">Live</span>
                </div>
                <div class="match-teams">
                    <div class="team">
                        <div class="team-name">India</div>
                        <div class="team-score">245/4 (45.2 ov)</div>
                    </div>
                    <div class="team">
                        <div class="team-name">Australia</div>
                        <div class="team-score">241/10 (47.5 ov)</div>
                    </div>
                </div>
                <div class="match-details">
                    <span>RR: 5.41</span>
                    <span>Need 3 runs in 29 balls</span>
                    <span>MOM: V Kohli</span>
                </div>
            </div>

            <div class="match-card">
                <div class="match-header">
                    <span>T20I • Match 5</span>
                    <span class="match-status">Live</span>
                </div>
                <div class="match-teams">
                    <div class="team">
                        <div class="team-name">England</div>
                        <div class="team-score">156/3 (14.0 ov)</div>
                    </div>
                    <div class="team">
                        <div class="team-name">Pakistan</div>
                        <div class="team-score">155/8 (20 ov)</div>
                    </div>
                </div>
                <div class="match-details">
                    <span>RR: 11.14</span>
                    <span>Target 156</span>
                </div>
            </div>
        </section>

        <!-- Fixtures & Results -->
        <div class="fixtures-results">
            <section class="section" id="schedule">
                <h3 class="section-title">
                    <i class="fas fa-calendar-alt"></i>
                    Today's Fixtures
                </h3>
                <div class="fixture-item">
                    <span>South Africa vs India • 1st Test</span>
                    <span>10:30 AM</span>
                </div>
                <div class="fixture-item">
                    <span>New Zealand vs Bangladesh • 2nd ODI</span>
                    <span>2:00 PM</span>
                </div>
            </section>

            <section class="section">
                <h3 class="section-title">
                    <i class="fas fa-trophy"></i>
                    Recent Results
                </h3>
                <div class="result-item">
                    <span>India won by 5 wkts</span>
                    <span>Yesterday</span>
                </div>
                <div class="result-item">
                    <span>Australia won by 3 runs</span>
                    <span>2 days ago</span>
                </div>
            </section>
        </div>

        <!-- News Section -->
        <section id="news">
            <h2 class="section-title">
                <i class="fas fa-newspaper"></i>
                Latest News
            </h2>
            <div class="news-grid">
                <div class="news-card">
                    <div class="news-image">
                        <i class="fas fa-cricket"></i>
                    </div>
                    <div class="news-content">
                        <h4 class="news-title">Kohli breaks record with 50th ODI century</h4>
                        <p>Virat Kohli becomes fastest to reach 50 ODI centuries...</p>
                        <small>2 hours ago</small>
                    </div>
                </div>
                <div class="news-card">
                    <div class="news-image">
                        <i class="fas fa-users"></i>
                    </div>
                    <div class="news-content">
                        <h4 class="news-title">World Test Championship final announced</h4>
                        <p>India vs Australia to face off in WTC final...</p>
                        <small>4 hours ago</small>
                    </div>
                </div>
                <div class="news-card">
                    <div class="news-image">
                        <i class="fas fa-chart-line"></i>
                    </div>
                    <div class="news-content">
                        <h4 class="news-title">ICC Rankings: India retains No.1 spot</h4>
                        <p>India maintains top position in Test rankings...</p>
                        <small>1 day ago</small>
                    </div>
                </div>
            </div>
        </section>
    </div>

    <script>
        // Live score updates simulation
        function updateLiveScores() {
            const scores = document.querySelectorAll('.team-score');
            scores.forEach(score => {
                const current = parseInt(score.textContent.match(/\d+/)?.[0] || 0);
                if (Math.random() > 0.7) {
                    score.textContent = (current + Math.floor(Math.random() * 2) + 1) + score.textContent.replace(/^\d+/, '');
                }
            });
        }

        // Auto-update every 10 seconds
        setInterval(updateLiveScores, 10000);

        // Search functionality
        const searchInput = document.querySelector('.search-box input');
        searchInput.addEventListener('input', function(e) {
            const query = e.target.value.toLowerCase();
            document.querySelectorAll('.match-card, .fixture-item, .result-item').forEach(item => {
                const text = item.textContent.toLowerCase();
                item.style.display = text.includes(query) ? 'block' : 'none';
            });
        });

        // Smooth scrolling for navigation links
        document.querySelectorAll('a[href^="#"]').forEach(anchor => {
            anchor.addEventListener('click', function (e) {
                e.preventDefault();
                document.querySelector(this.getAttribute('href')).scrollIntoView({
                    behavior: 'smooth'
                });
            });
        });

        // Add live indicator pulse effect
        document.querySelectorAll('.live-indicator').forEach(el => {
            el.style.animation = 'pulse 2s infinite';
        });
    </script>
</body>
</html>
