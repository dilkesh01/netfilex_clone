<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Netflix Clone</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;600;700&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Montserrat', 'Helvetica Neue', Arial, sans-serif;
        }
        
        body {
            background-color: #141414;
            color: white;
            overflow-x: hidden;
        }
        
        /* Navbar */
        .navbar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 25px 50px;
            position: fixed;
            width: 100%;
            z-index: 100;
            transition: all 0.5s ease;
            background: linear-gradient(to bottom, rgba(0,0,0,0.7) 0%, rgba(0,0,0,0) 100%);
        }
        
        .navbar.scrolled {
            background-color: #141414;
            padding: 15px 50px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.3);
        }
        
        .logo {
            height: 45px;
            transition: all 0.3s ease;
        }
        
        .navbar.scrolled .logo {
            height: 35px;
        }
        
        .nav-right {
            display: flex;
            align-items: center;
            gap: 25px;
        }
        
        .nav-links {
            display: flex;
            gap: 25px;
            list-style: none;
        }
        
        .nav-links li a {
            color: white;
            text-decoration: none;
            font-size: 15px;
            font-weight: 500;
            transition: all 0.3s ease;
            position: relative;
        }
        
        .nav-links li a:hover {
            color: #e50914;
        }
        
        .nav-links li a::after {
            content: '';
            position: absolute;
            width: 0;
            height: 2px;
            bottom: -5px;
            left: 0;
            background-color: #e50914;
            transition: width 0.3s ease;
        }
        
        .nav-links li a:hover::after {
            width: 100%;
        }
        
        .profile {
            height: 35px;
            border-radius: 4px;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        .profile:hover {
            transform: scale(1.1);
        }
        
        /* Hero Section */
        .hero {
            height: 100vh;
            background: linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)), 
                        url('https://assets.nflxext.com/ffe/siteui/vlv3/9d3533b2-0e2b-40b2-95e0-ecd7979cc88b/a3873901-5b7c-46eb-b9fa-12fea5197bd3/IN-en-20240311-popsignuptwoweeks-perspective_alpha_website_large.jpg');
            background-size: cover;
            background-position: center;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
            padding: 0 20px;
            position: relative;
        }
        
        .hero-content {
            max-width: 800px;
            z-index: 2;
            animation: fadeInUp 1s ease;
        }
        
        .hero h1 {
            font-size: 3.5rem;
            margin-bottom: 20px;
            text-shadow: 2px 2px 5px rgba(0,0,0,0.5);
            line-height: 1.2;
        }
        
        .hero h2 {
            font-size: 1.8rem;
            font-weight: 400;
            margin-bottom: 30px;
            text-shadow: 1px 1px 3px rgba(0,0,0,0.5);
        }
        
        .hero p {
            font-size: 1.3rem;
            margin-bottom: 30px;
            text-shadow: 1px 1px 2px rgba(0,0,0,0.5);
        }
        
        .email-signup {
            display: flex;
            gap: 10px;
            width: 100%;
            max-width: 650px;
            margin: 0 auto;
        }
        
        .email-signup input {
            flex: 1;
            padding: 18px;
            border: none;
            border-radius: 4px;
            background-color: rgba(0, 0, 0, 0.7);
            color: white;
            border: 1px solid #444;
            font-size: 16px;
            transition: all 0.3s ease;
        }
        
        .email-signup input:focus {
            outline: none;
            border-color: #e50914;
            background-color: rgba(0, 0, 0, 0.9);
        }
        
        .email-signup button {
            padding: 0 30px;
            background-color: #e50914;
            color: white;
            border: none;
            border-radius: 4px;
            font-size: 1.5rem;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .email-signup button:hover {
            background-color: #f40612;
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0,0,0,0.3);
        }
        
        /* Movie Rows */
        .movie-section {
            padding: 60px 50px;
            position: relative;
        }
        
        .section-title {
            font-size: 1.8rem;
            margin-bottom: 25px;
            font-weight: 700;
            position: relative;
            display: inline-block;
        }
        
        .section-title::after {
            content: '';
            position: absolute;
            width: 50%;
            height: 3px;
            bottom: -8px;
            left: 0;
            background-color: #e50914;
            border-radius: 3px;
        }
        
        .movie-row {
            display: flex;
            overflow-x: auto;
            gap: 15px;
            padding: 25px 0;
            scrollbar-width: none;
            scroll-behavior: smooth;
        }
        
        .movie-row::-webkit-scrollbar {
            display: none;
        }
        
        .movie-item {
            min-width: 220px;
            transition: transform 0.3s ease;
            position: relative;
            border-radius: 8px;
            overflow: hidden;
            box-shadow: 0 5px 15px rgba(0,0,0,0.3);
        }
        
        .movie-item:hover {
            transform: scale(1.08);
            z-index: 10;
        }
        
        .movie-item img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            transition: all 0.5s ease;
        }
        
        .movie-item:hover img {
            transform: scale(1.1);
        }
        
        .movie-info {
            position: absolute;
            bottom: 0;
            left: 0;
            right: 0;
            background: linear-gradient(to top, rgba(0,0,0,0.9) 0%, rgba(0,0,0,0) 100%);
            padding: 20px;
            opacity: 0;
            transition: all 0.3s ease;
            transform: translateY(20px);
        }
        
        .movie-item:hover .movie-info {
            opacity: 1;
            transform: translateY(0);
        }
        
        .movie-title {
            font-weight: 600;
            margin-bottom: 5px;
        }
        
        .movie-meta {
            display: flex;
            gap: 10px;
            font-size: 0.8rem;
            color: #ccc;
        }
        
        .movie-rating {
            color: #e50914;
            font-weight: bold;
        }
        
        .scroll-arrows {
            position: absolute;
            top: 50%;
            transform: translateY(-50%);
            width: 40px;
            height: 40px;
            background-color: rgba(0,0,0,0.7);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            z-index: 5;
            opacity: 0;
            transition: all 0.3s ease;
        }
        
        .scroll-left {
            left: 10px;
        }
        
        .scroll-right {
            right: 10px;
        }
        
        .movie-section:hover .scroll-arrows {
            opacity: 1;
        }
        
        .scroll-arrows:hover {
            background-color: rgba(229,9,20,0.8);
        }
        
        /* Featured Banner */
        .featured-banner {
            position: relative;
            height: 70vh;
            margin-bottom: 50px;
            overflow: hidden;
        }
        
        .featured-background {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-size: cover;
            background-position: center;
            filter: brightness(0.5);
            z-index: 1;
        }
        
        .featured-content {
            position: relative;
            z-index: 2;
            height: 100%;
            display: flex;
            flex-direction: column;
            justify-content: center;
            padding: 0 80px;
            max-width: 50%;
        }
        
        .featured-logo {
            max-width: 400px;
            margin-bottom: 20px;
        }
        
        .featured-description {
            font-size: 1.2rem;
            margin-bottom: 20px;
            line-height: 1.5;
        }
        
        .featured-buttons {
            display: flex;
            gap: 15px;
        }
        
        .featured-button {
            padding: 10px 25px;
            border-radius: 4px;
            font-weight: 600;
            display: flex;
            align-items: center;
            gap: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        .play-button {
            background-color: white;
            color: black;
        }
        
        .play-button:hover {
            background-color: rgba(255,255,255,0.8);
        }
        
        .info-button {
            background-color: rgba(109, 109, 110, 0.7);
            color: white;
        }
        
        .info-button:hover {
            background-color: rgba(109, 109, 110, 0.5);
        }
        
        /* Footer */
        footer {
            padding: 70px 50px 30px;
            background-color: #000;
            color: #757575;
        }
        
        .footer-content {
            max-width: 1000px;
            margin: 0 auto;
        }
        
        .social-icons {
            display: flex;
            gap: 20px;
            margin-bottom: 30px;
        }
        
        .social-icon {
            font-size: 1.8rem;
            color: #757575;
            transition: all 0.3s ease;
            cursor: pointer;
        }
        
        .social-icon:hover {
            color: #e50914;
            transform: translateY(-3px);
        }
        
        .footer-links {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 20px;
            margin: 30px 0;
        }
        
        .footer-links a {
            color: #757575;
            text-decoration: none;
            font-size: 14px;
            transition: all 0.3s ease;
        }
        
        .footer-links a:hover {
            color: #e50914;
            text-decoration: underline;
        }
        
        .footer-bottom {
            margin-top: 30px;
            font-size: 14px;
        }
        
        /* Animations */
        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        
        /* Responsive */
        @media (max-width: 1024px) {
            .featured-content {
                max-width: 70%;
            }
        }
        
        @media (max-width: 768px) {
            .navbar {
                padding: 20px;
            }
            
            .nav-links {
                display: none;
            }
            
            .hero h1 {
                font-size: 2.5rem;
            }
            
            .hero h2 {
                font-size: 1.3rem;
            }
            
            .email-signup {
                flex-direction: column;
            }
            
            .email-signup button {
                padding: 15px 30px;
                justify-content: center;
            }
            
            .movie-section {
                padding: 40px 20px;
            }
            
            .movie-item {
                min-width: 180px;
            }
            
            .featured-content {
                max-width: 90%;
                padding: 0 40px;
            }
            
            .featured-logo {
                max-width: 300px;
            }
            
            .footer-links {
                grid-template-columns: repeat(2, 1fr);
            }
        }
        
        @media (max-width: 480px) {
            .hero h1 {
                font-size: 2rem;
            }
            
            .hero h2 {
                font-size: 1.1rem;
            }
            
            .movie-item {
                min-width: 150px;
            }
            
            .featured-content {
                padding: 0 20px;
            }
            
            .featured-logo {
                max-width: 200px;
            }
            
            .featured-buttons {
                flex-direction: column;
            }
        }
    </style>
</head>
<body>
    <!-- Navbar -->
    <nav class="navbar">
        <img src="https://upload.wikimedia.org/wikipedia/commons/0/08/Netflix_2015_logo.svg" alt="Netflix Logo" class="logo">
        <div class="nav-right">
            <ul class="nav-links">
                <li><a href="#">Home</a></li>
                <li><a href="#">TV Shows</a></li>
                <li><a href="#">Movies</a></li>
                <li><a href="#">New & Popular</a></li>
                <li><a href="#">My List</a></li>
                <li><a href="#">Sign in</a></li>
            </ul>
            <img src="https://upload.wikimedia.org/wikipedia/commons/0/0b/Netflix-avatar.png" alt="Profile" class="profile">
        </div>
    </nav>
    
    <!-- Hero Section -->
    <section class="hero">
        <div class="hero-content">
            <h1>Unlimited movies, TV shows and more</h1>
            <h2>Watch anywhere. Cancel anytime.</h2>
            <p>Ready to watch? Enter your email to create or restart your membership.</p>
            <div class="email-signup">
                <input type="email" placeholder="Email address">
                <button>Get Started <i class="fas fa-chevron-right"></i></button>
            </div>
        </div>
    </section>
    
    <!-- Featured Banner -->
    <section class="featured-banner">
        <div class="featured-background" style="background-image: url('https://image.tmdb.org/t/p/original/1XDDXPXGiI8id7MrUxK36ke7gkX.jpg');"></div>
        <div class="featured-content">
            <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/7/77/Breaking_Bad_logo.svg/1200px-Breaking_Bad_logo.svg.png" alt="Breaking Bad" class="featured-logo">
            <p class="featured-description">A high school chemistry teacher diagnosed with inoperable lung cancer turns to manufacturing and selling methamphetamine in order to secure his family's future.</p>
            <div class="featured-buttons">
                <div class="featured-button play-button">
                    <i class="fas fa-play"></i> Play
                </div>
                <div class="featured-button info-button">
                    <i class="fas fa-info-circle"></i> More Info
                </div>
            </div>
        </div>
    </section>
    
    <!-- Movie Rows -->
    <section class="movie-section">
        <h2 class="section-title">Popular on Netflix</h2>
        <div class="scroll-arrows scroll-left"><i class="fas fa-chevron-left"></i></div>
        <div class="scroll-arrows scroll-right"><i class="fas fa-chevron-right"></i></div>
        <div class="movie-row" id="popular-row">
            <div class="movie-item">
                <img src="https://image.tmdb.org/t/p/w500/1pdfLvkbY9ohJlCjQH2CZjjYVvJ.jpg" alt="Stranger Things">
                <div class="movie-info">
                    <div class="movie-title">Stranger Things</div>
                    <div class="movie-meta">
                        <span class="movie-rating">94% Match</span>
                        <span>4 Seasons</span>
                    </div>
                </div>
            </div>
            <div class="movie-item">
                <img src="https://image.tmdb.org/t/p/w500/9dKCd55IuTT5QRs989m9Qlb7d2B.jpg" alt="The Witcher">
                <div class="movie-info">
                    <div class="movie-title">The Witcher</div>
                    <div class="movie-meta">
                        <span class="movie-rating">89% Match</span>
                        <span>3 Seasons</span>
                    </div>
                </div>
            </div>
            <div class="movie-item">
                <img src="https://image.tmdb.org/t/p/w500/8Vt6mWEReuy4Of61Lnj5Xj704m8.jpg" alt="Money Heist">
                <div class="movie-info">
                    <div class="movie-title">Money Heist</div>
                    <div class="movie-meta">
                        <span class="movie-rating">92% Match</span>
                        <span>5 Seasons</span>
                    </div>
                </div>
            </div>
            <div class="movie-item">
                <img src="https://image.tmdb.org/t/p/w500/7gKI9hpEMcZUQpNgKrkDzJpbnNS.jpg" alt="Dark">
                <div class="movie-info">
                    <div class="movie-title">Dark</div>
                    <div class="movie-meta">
                        <span class="movie-rating">96% Match</span>
                        <span>3 Seasons</span>
                    </div>
                </div>
            </div>
            <div class="movie-item">
                <img src="https://image.tmdb.org/t/p/w500/1LRLLWGvs5sZdTzuMqLEahb88Pc.jpg" alt="The Queen's Gambit">
                <div class="movie-info">
                    <div class="movie-title">The Queen's Gambit</div>
                    <div class="movie-meta">
                        <span class="movie-rating">98% Match</span>
                        <span>Limited Series</span>
                    </div>
                </div>
            </div>
            <div class="movie-item">
                <img src="https://image.tmdb.org/t/p/w500/8Gxv8gSFCU0XGDykEGv7zR1n2ua.jpg" alt="Squid Game">
                <div class="movie-info">
                    <div class="movie-title">Squid Game</div>
                    <div class="movie-meta">
                        <span class="movie-rating">95% Match</span>
                        <span>1 Season</span>
                    </div>
                </div>
            </div>
            <div class="movie-item">
                <img src="https://image.tmdb.org/t/p/w500/6kbAMLteGO8yyewYau6bJ683sw7.jpg" alt="The Crown">
                <div class="movie-info">
                    <div class="movie-title">The Crown</div>
                    <div class="movie-meta">
                        <span class="movie-rating">91% Match</span>
                        <span>5 Seasons</span>
                    </div>
                </div>
            </div>
        </div>
    </section>
    
    <section class="movie-section">
        <h2 class="section-title">Trending Now</h2>
        <div class="scroll-arrows scroll-left"><i class="fas fa-chevron-left"></i></div>
        <div class="scroll-arrows scroll-right"><i class="fas fa-chevron-right"></i></div>
        <div class="movie-row" id="trending-row">
            <div class="movie-item">
                <img src="https://image.tmdb.org/t/p/w500/1XDDXPXGiI8id7MrUxK36ke7gkX.jpg" alt="Breaking Bad">
                <div class="movie-info">
                    <div class="movie-title">Breaking Bad</div>
                    <div class="movie-meta">
                        <span class="movie-rating">99% Match</span>
                        <span>5 Seasons</span>
                    </div>
                </div>
            </div>
            <div class="movie-item">
                <img src="https://image.tmdb.org/t/p/w500/8Vt6mWEReuy4Of61Lnj5Xj704m8.jpg" alt="Money Heist">
                <div class="movie-info">
                    <div class="movie-title">Money Heist</div>
                    <div class="movie-meta">
                        <span class="movie-rating">92% Match</span>
                        <span>5 Seasons</span>
                    </div>
                </div>
            </div>
            <div class="movie-item">
                <img src="https://image.tmdb.org/t/p/w500/7gKI9hpEMcZUQpNgKrkDzJpbnNS.jpg" alt="Dark">
                <div class="movie-info">
                    <div class="movie-title">Dark</div>
                    <div class="movie-meta">
                        <span class="movie-rating">96% Match</span>
                        <span>3 Seasons</span>
                    </div>
                </div>
            </div>
            <div class="movie-item">
                <img src="https://image.tmdb.org/t/p/w500/9dKCd55IuTT5QRs989m9Qlb7d2B.jpg" alt="The Witcher">
                <div class="movie-info">
                    <div class="movie-title">The Witcher</div>
                    <div class="movie-meta">
                        <span class="movie-rating">89% Match</span>
                        <span>3 Seasons</span>
                    </div>
                </div>
            </div>
            <div class="movie-item">
                <img src="https://image.tmdb.org/t/p/w500/1pdfLvkbY9ohJlCjQH2CZjjYVvJ.jpg" alt="Stranger Things">
                <div class="movie-info">
                    <div class="movie-title">Stranger Things</div>
                    <div class="movie-meta">
                        <span class="movie-rating">94% Match</span>
                        <span>4 Seasons</span>
                    </div>
                </div>
            </div>
            <div class="movie-item">
                <img src="https://image.tmdb.org/t/p/w500/8Gxv8gSFCU0XGDykEGv7zR1n2ua.jpg" alt="Squid Game">
                <div class="movie-info">
                    <div class="movie-title">Squid Game</div>
                    <div class="movie-meta">
                        <span class="movie-rating">95% Match</span>
                        <span>1 Season</span>
                    </div>
                </div>
            </div>
            <div class="movie-item">
                <img src="https://image.tmdb.org/t/p/w500/edv5h6XigDolLBBrFvKfgWY3D0V.jpg" alt="Peaky Blinders">
                <div class="movie-info">
                    <div class="movie-title">Peaky Blinders</div>
                    <div class="movie-meta">
                        <span class="movie-rating">93% Match</span>
                        <span>6 Seasons</span>
                    </div>
                </div>
            </div>
        </div>
    </section>
    
    <section class="movie-section">
        <h2 class="section-title">Continue Watching</h2>
        <div class="scroll-arrows scroll-left"><i class="fas fa-chevron-left"></i></div>
        <div class="scroll-arrows scroll-right"><i class="fas fa-chevron-right"></i></div>
        <div class="movie-row" id="continue-row">
            <div class="movie-item">
                <img src="https://image.tmdb.org/t/p/w500/8Gxv8gSFCU0XGDykEGv7zR1n2ua.jpg" alt="Squid Game">
                <div class="movie-info">
                    <div class="movie-title">Squid Game</div>
                    <div class="movie-meta">
                        <span>Episode 5</span>
                        <span>45% watched</span>
                    </div>
                    <div class="progress-bar">
                        <div class="progress" style="width: 45%;"></div>
                    </div>
                </div>
            </div>
            <div class="movie-item">
                <img src="https://image.tmdb.org/t/p/w500/1pdfLvkbY9ohJlCjQH2CZjjYVvJ.jpg" alt="Stranger Things">
                <div class="movie-info">
                    <div class="movie-title">Stranger Things</div>
                    <div class="movie-meta">
                        <span>Episode 3</span>
                        <span>72% watched</span>
                    </div>
                    <div class="progress-bar">
                        <div class="progress" style="width: 72%;"></div>
                    </div>
                </div>
            </div>
            <div class="movie-item">
                <img src="https://image.tmdb.org/t/p/w500/9dKCd55IuTT5QRs989m9Qlb7d2B.jpg" alt="The Witcher">
                <div class="movie-info">
                    <div class="movie-title">The Witcher</div>
                    <div class="movie-meta">
                        <span>Episode 7</span>
                        <span>15% watched</span>
                    </div>
                    <div class="progress-bar">
                        <div class="progress" style="width: 15%;"></div>
                    </div>
                </div>
            </div>
            <div class="movie-item">
                <img src="https://image.tmdb.org/t/p/w500/8Vt6mWEReuy4Of61Lnj5Xj704m8.jpg" alt="Money Heist">
                <div class="movie-info">
                    <div class="movie-title">Money Heist</div>
                    <div class="movie-meta">
                        <span>Episode 9</span>
                        <span>90% watched</span>
                    </div>
                    <div class="progress-bar">
                        <div class="progress" style="width: 90%;"></div>
                    </div>
                </div>
            </div>
            <div class="movie-item">
                <img src="https://image.tmdb.org/t/p/w500/7gKI9hpEMcZUQpNgKrkDzJpbnNS.jpg" alt="Dark">
                <div class="movie-info">
                    <div class="movie-title">Dark</div>
                    <div class="movie-meta">
                        <span>Episode 2</span>
                        <span>30% watched</span>
                    </div>
                    <div class="progress-bar">
                        <div class="progress" style="width: 30%;"></div>
                    </div>
                </div>
            </div>
            <div class="movie-item">
                <img src="https://image.tmdb.org/t/p/w500/1XDDXPXGiI8id7MrUxK36ke7gkX.jpg" alt="Breaking Bad">
                <div class="movie-info">
                    <div class="movie-title">Breaking Bad</div>
                    <div class="movie-meta">
                        <span>Episode 12</span>
                        <span>65% watched</span>
                    </div>
                    <div class="progress-bar">
                        <div class="progress" style="width: 65%;"></div>
                    </div>
                </div>
            </div>
            <div class="movie-item">
                <img src="https://image.tmdb.org/t/p/w500/edv5h6XigDolLBBrFvKfgWY3D0V.jpg" alt="Peaky Blinders">
                <div class="movie-info">
                    <div class="movie-title">Peaky Blinders</div>
                    <div class="movie-meta">
                        <span>Episode 4</span>
                        <span>20% watched</span>
                    </div>
                    <div class="progress-bar">
                        <div class="progress" style="width: 20%;"></div>
                    </div>
                </div>
            </div>
        </div>
    </section>
    
    <!-- Footer -->
    <footer>
        <div class="footer-content">
            <div class="social-icons">
                <i class="fab fa-facebook social-icon"></i>
                <i class="fab fa-instagram social-icon"></i>
                <i class="fab fa-twitter social-icon"></i>
                <i class="fab fa-youtube social-icon"></i>
            </div>
            <div class="footer-links">
                <a href="#">FAQ</a>
                <a href="#">Help Center</a>
                <a href="#">Account</a>
                <a href="#">Media Center</a>
                <a href="#">Investor Relations</a>
                <a href="#">Jobs</a>
                <a href="#">Ways to Watch</a>
                <a href="#">Terms of Use</a>
                <a href="#">Privacy</a>
                <a href="#">Cookie Preferences</a>
                <a href="#">Corporate Information</a>
                <a href="#">Contact Us</a>
                <a href="#">Speed Test</a>
                <a href="#">Legal Notices</a>
                <a href="#">Only on Netflix</a>
            </div>
            <div class="footer-bottom">
                <p>Netflix Clone - This is a netflix website for joy and enjoy life.</p>
                <p>&copy; 2025 Netflix Clone. All rights reserved.</p>
            </div>
        </div>
    </footer>
    
    <script>
        // Navbar scroll effect
        window.addEventListener('scroll', () => {
            const navbar = document.querySelector('.navbar');
            if (window.scrollY > 100) {
                navbar.classList.add('scrolled');
            } else {
                navbar.classList.remove('scrolled');
            }
        });
        
        // Scroll functionality for movie rows
        document.querySelectorAll('.scroll-arrows').forEach(arrow => {
            arrow.addEventListener('click', (e) => {
                const direction = e.target.closest('.scroll-arrows').classList.contains('scroll-left') ? -1 : 1;
                const row = e.target.closest('.movie-section').querySelector('.movie-row');
                row.scrollBy({
                    left: direction * 300,
                    behavior: 'smooth'
                });
            });
        });
        
        // Hover effect for movie items
        document.querySelectorAll('.movie-item').forEach(item => {
            item.addEventListener('mouseenter', () => {
                const info = item.querySelector('.movie-info');
                info.style.opacity = '1';
                info.style.transform = 'translateY(0)';
            });
            
            item.addEventListener('mouseleave', () => {
                const info = item.querySelector('.movie-info');
                info.style.opacity = '0';
                info.style.transform = 'translateY(20px)';
            });
        });
        
        // Email signup animation
        const emailInput = document.querySelector('.email-signup input');
        const emailButton = document.querySelector('.email-signup button');
        
        emailInput.addEventListener('focus', () => {
            emailButton.style.transform = 'translateY(-2px)';
            emailButton.style.boxShadow = '0 5px 15px rgba(0,0,0,0.3)';
        });
        
        emailInput.addEventListener('blur', () => {
            emailButton.style.transform = 'translateY(0)';
            emailButton.style.boxShadow = 'none';
        });
        
        // Featured banner buttons
        document.querySelector('.play-button').addEventListener('click', () => {
            alert('Play button clicked! This would start playback in a real app.');
        });
        
        document.querySelector('.info-button').addEventListener('click', () => {
            alert('More info button clicked! This would show more details in a real app.');
        });
    </script>
</body>
</html>
