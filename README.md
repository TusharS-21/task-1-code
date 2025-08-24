<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="TravX - Your one-stop travel booking platform for flights, hotels, and vacation packages with best price guarantee">
    <title>TravX - Your Complete Travel Solution</title>
    <style>
        /* Base Styles - Optimized */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        body {
            font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', sans-serif;
        }

        body {
            padding-top: 80px;
            line-height: 1.6;
            color: #333;
            background-color: #f8f9fa;
            transition: all 0.3s ease;
            scroll-behavior: smooth;
        }

        section {
            min-height: 100vh;
            padding: 4rem 2rem;
            display: flex;
            justify-content: center;
            align-items: center;
            flex-direction: column;
            text-align: center;
            position: relative;
            background-size: cover;
            background-position: center;
            color: #fff;
            overflow: hidden;
            will-change: transform; /* Hint browser to optimize */
            contain: content; /* Limit repaint/reflow area */
        }
        
        /* No overlay for flights section only */
        section:not(#flights)::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0,0,0,0.6);
            z-index: 1;
        }
        
        section > * {
            position: relative;
            z-index: 2;
        }

        section h2 {
            font-size: 2.5rem;
            margin-bottom: 1.5rem;
            font-weight: 600;
            color: white;
            opacity: 0;
            transform: translateY(20px);
            transition: all 0.5s ease;
            text-shadow: 1px 1px 2px rgba(0,0,0,0.3);
        }

        section p {
            max-width: 800px;
            color: white;
            font-size: 1.1rem;
            line-height: 1.8;
            margin: 0 auto 2rem;
            opacity: 0;
            transform: translateY(20px);
            transition: all 0.5s ease 0.2s;
            font-weight: 500;
            text-shadow: 1px 1px 2px rgba(0,0,0,0.3);
        }

        section.in-view h2,
        section.in-view p {
            opacity: 1;
            transform: translateY(0);
        }

        /* Navigation Styles */
        nav {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 80px;
            background-color: rgba(255, 255, 255, 0.95);
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
            transition: all 0.3s ease;
            z-index: 1000;
        }

        .scrolled {
            background-color: rgba(30, 41, 59, 0.9);
            height: 60px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.3);
            backdrop-filter: blur(5px);
        }

        .scrolled .logo {
            color: white;
            transform: scale(0.9);
        }

        .scrolled .nav-links li a {
            color: #f8fafc;
        }

        .nav-container {
            max-width: 1200px;
            height: 100%;
            margin: 0 auto;
            padding: 0 2rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .logo {
            font-size: 1.8rem;
            font-weight: 700;
            color: #1e293b;
            text-decoration: none;
            transition: all 0.3s ease;
        }

        .nav-links {
            display: flex;
            list-style: none;
        }

        .nav-links li {
            margin-left: 2rem;
            position: relative;
        }

        .nav-links li a {
            text-decoration: none;
            color: #334155;
            font-weight: 500;
            font-size: 1.1rem;
            transition: all 0.3s ease;
            padding: 0.5rem 0;
            position: relative;
        }

        /* Hover Effects */
        .nav-links li a:hover {
            color: #3b82f6;
        }

        .scrolled .nav-links li a:hover {
            color: #60a5fa;
        }

        /* Underline animation */
        .nav-links li a::after {
            content: '';
            position: absolute;
            width: 0;
            height: 2px;
            bottom: 0;
            left: 0;
            background-color: #3b82f6;
            transition: width 0.3s ease;
        }

        .scrolled .nav-links li a::after {
            background-color: #60a5fa;
        }

        .nav-links li a:hover::after {
            width: 100%;
        }

        /* Mobile menu toggle */
        .hamburger {
            display: none;
            cursor: pointer;
        }

        .hamburger div {
            width: 25px;
            height: 3px;
            background-color: #1e293b;
            margin: 5px;
            transition: all 0.3s ease;
        }

        .scrolled .hamburger div {
            background-color: white;
        }

        /* Responsive Design */
        @media screen and (max-width: 768px) {
            body {
                padding-top: 60px;
            }

            .hamburger {
                display: block;
            }

            .nav-links {
                position: absolute;
                top: 60px;
                left: 0;
                width: 100%;
                background-color: rgba(255, 255, 255, 0.95);
                flex-direction: column;
                align-items: center;
                padding: 1rem 0;
                clip-path: circle(0px at 90% -10%);
                transition: all 0.5s ease-out;
                pointer-events: none;
            }

            .scrolled .nav-links {
                top: 60px;
                background-color: rgba(30, 41, 59, 0.98);
            }

            .nav-links.open {
                clip-path: circle(1000px at 90% -10%);
                pointer-events: all;
            }

            .nav-links li {
                margin: 1rem 0;
                opacity: 0;
            }

            .nav-links li a {
                color: #334155;
            }

            .scrolled .nav-links li a {
                color: #f8fafc;
            }

            .nav-links li:nth-child(1) {
                transition: all 0.5s ease 0.2s;
            }

            .nav-links li:nth-child(2) {
                transition: all 0.5s ease 0.3s;
            }

            .nav-links li:nth-child(3) {
                transition: all 0.5s ease 0.4s;
            }

            .nav-links li:nth-child(4) {
                transition: all 0.5s ease 0.5s;
            }

            .nav-links li.fade {
                opacity: 1;
            }
        }

        /* Button Styles */
        .cta-buttons {
            display: flex;
            gap: 1rem;
            margin-top: 2rem;
        }

        .cta-btn {
            padding: 0.8rem 1.5rem;
            border-radius: 4px;
            font-weight: 500;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .primary {
            background-color: #3b82f6;
            color: white;
            border: none;
            font-weight: 600;
            padding: 1rem 2rem;
            font-size: 1.1rem;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
        }

        .primary:hover {
            background-color: #2563eb;
            transform: translateY(-2px);
        }

        .secondary {
            background: transparent;
            border: 2px solid #3b82f6;
            color: #3b82f6;
        }

        .secondary:hover {
            background-color: rgba(59, 130, 246, 0.1);
            transform: translateY(-2px);
        }

        .clicked {
            transform: scale(0.95) !important;
        }

        .features {
            display: flex;
            justify-content: center;
            gap: 2rem;
            margin-top: 3rem;
            flex-wrap: wrap;
        }

        .feature-item {
            background: rgba(255,255,255,0.1);
            padding: 1.5rem;
            border-radius: 8px;
            text-align: center;
            max-width: 200px;
            backdrop-filter: blur(5px);
        }

        .feature-item .icon {
            font-size: 2rem;
            margin-bottom: 1rem;
            display: block;
        }

        .feature-item h3 {
            margin-bottom: 0.5rem;
            color: white;
        }

        .feature-item p {
            font-size: 0.9rem;
            margin: 0;
        }

        /* Task Section Styles */
        .task-container {
            background: rgba(255,255,255,0.9);
            padding: 2rem;
            border-radius: 8px;
            box-shadow: 0 4px 20px rgba(0,0,0,0.15);
            max-width: 800px;
            margin: 0 auto;
            color: #333;
        }
        
        .task-container h3 {
            color: #2c3e50;
            margin-bottom: 1rem;
        }
        
        .task-container p {
            color: #555;
            margin-bottom: 1.5rem;
        }

        .task-image {
            width: 100%;
            max-height: 300px;
            object-fit: cover;
            border-radius: 4px;
            margin-bottom: 1rem;
        }

        .task-buttons {
            display: flex;
            gap: 1rem;
            justify-content: center;
            flex-wrap: wrap;
            margin-top: 2rem;
        }

        .task-btn {
            padding: 0.8rem 1.2rem;
            background: #3b82f6;
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            transition: all 0.2s ease;
        }

        .task-btn:hover {
            background: #2563eb;
            transform: translateY(-2px);
        }

        /* Booking form styles */
        .booking-container {
            background: rgba(255,255,255,0.9);
            padding: 2rem;
            border-radius: 8px;
            max-width: 600px;
            margin: 0 auto;
        }

        .booking-form {
            margin-top: 2rem;
        }

        .form-group {
            margin-bottom: 1rem;
            text-align: left;
        }

        .form-group label {
            display: block;
            margin-bottom: 0.5rem;
            color: #333;
            font-weight: 500;
        }

        .form-group input,
        .form-group select {
            width: 100%;
            padding: 0.8rem;
            border: 1px solid #ddd;
            border-radius: 4px;
        }

        .form-row {
            display: flex;
            gap: 1rem;
        }

        .form-row .form-group {
            flex: 1;
        }

        .search-btn {
            width: 100%;
            padding: 1rem;
            background: #ff6e1f;
            color: white;
            border: none;
            border-radius: 4px;
            font-size: 1.1rem;
            font-weight: 600;
            cursor: pointer;
            margin-top: 1.5rem;
            box-shadow: 0 4px 8px rgba(0,0,0,0.1);
            transition: all 0.3s ease;
        }

        .popular-tags {
            margin-top: 1.5rem;
            display: flex;
            flex-wrap: wrap;
            gap: 0.5rem;
            align-items: center;
        }

        .popular-tags span {
            font-weight: 500;
            color: #444;
            margin-right: 0.5rem;
        }

        .popular-tags a {
            padding: 0.5rem 1rem;
            background: #f0f0f0;
            border-radius: 20px;
            color: #333;
            text-decoration: none;
            font-size: 0.9rem;
            transition: all 0.2s ease;
        }

        .popular-tags a:hover {
            background: #e0e0e0;
            color: #000;
        }

        .search-btn:hover {
            background: #e55b12;
        }

        /* Footer Styles */
        footer {
            background: #2c3e50;
            color: white;
            padding: 2rem;
            text-align: center;
        }

        .footer-content {
            max-width: 1200px;
            margin: 0 auto;
            display: flex;
            flex-direction: column;
            gap: 1rem;
        }

        .footer-links {
            display: flex;
            justify-content: center;
            gap: 2rem;
        }

        .footer-links a {
            color: #ecf0f1;
            text-decoration: none;
            transition: color 0.3s ease;
        }

        .footer-links a:hover {
            color: #3b82f6;
        }
    </style>
</head>
<body>
    <!-- Navigation -->
    <nav id="navbar">
        <div class="nav-container">
            <a href="#" class="logo">TravX</a>
            <div class="hamburger">
                <div class="line1"></div>
                <div class="line2"></div>
                <div class="line3"></div>
            </div>
            <ul class="nav-links">
                <li><a href="#home">Home</a></li>
                <li><a href="#flights">Flights</a></li>
                <li><a href="#hotels">Hotels</a></li>
                <li><a href="#packages">Packages</a></li>
                <li><a href="#contact">Contact</a></li>
                <li><a href="#login">Login</a></li>
            </ul>
        </div>
    </nav>

    <!-- Demo sections for scrolling -->
    <section id="home" style="background-image: url('https://images.unsplash.com/photo-1507525428034-b723cf961d3e?ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80')">
        <h2>Discover Your Next Adventure</h2>
        <p>TravX is a premium travel booking platform offering seamless reservations for flights, hotels, and vacation packages worldwide. Our best price guarantee ensures you always get the most value for your dream vacation.</p>
        <div class="features">
            <div class="feature-item">
                <i class="icon">✈️</i>
                <h3>500+ Airlines</h3>
                <p>Compare prices across major carriers</p>
            </div>
            <div class="feature-item">
                <i class="icon">🏨</i>
                <h3>100k+ Hotels</h3>
                <p>From budget to luxury accommodations</p>
            </div>
            <div class="feature-item">
                <i class="icon">🌴</i>
                <h3>24/7 Support</h3>
                <p>Dedicated travel experts available anytime</p>
            </div>
        </div>
        <div class="cta-buttons">
            <button class="cta-btn primary">Book Now</button>
            <button class="cta-btn secondary">Learn More</button>
        </div>
    </section>

    <section id="task-section" style="background-image: linear-gradient(rgba(0, 102, 204, 0.7), rgba(0, 102, 204, 0.7)), url('https://images.unsplash.com/photo-1499678329936-a4c03b9a6a93?ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80')">
        <div class="task-container">
            <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/36d1d747-b8b6-4904-86ad-7f0e3e8654cd.png" alt="TravX Special Task" class="task-image">
            <h3>TravX Task - Special Booking System</h3>
            <p>Exclusive booking interface for your travel needs</p>
            <div class="task-buttons">
                <button class="task-btn">Book Flights</button>
                <button class="task-btn">Reserve Hotels</button>
                <button class="task-btn">Custom Packages</button>
            </div>
        </div>
    </section>

    <section id="flights" style="background-image: linear-gradient(rgba(255,255,255,0.5), rgba(255,255,255,0.5)), url('https://images.unsplash.com/photo-1436491865332-7a61a109cc05?ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80')">
        <h2>Flight Bookings</h2>
        <p>Search and compare flights from hundreds of airlines worldwide. We guarantee the best prices for your next trip.</p>
    </section>

    <section id="hotels" style="background-image: linear-gradient(rgba(0, 102, 204, 0.7), rgba(0, 102, 204, 0.7)), url('https://images.unsplash.com/photo-1566073771259-6a8509689948?ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80')">
        <div class="booking-container">
            <h2>Hotel Bookings</h2>
            <div class="booking-form">
                <div class="form-group">
                    <label>Destination</label>
                    <input type="text" placeholder="Enter city or hotel">
                </div>
                <div class="form-row">
                    <div class="form-group">
                        <label>Check-in</label>
                        <input type="date">
                    </div>
                    <div class="form-group">
                        <label>Check-out</label>
                        <input type="date">
                    </div>
                </div>
                <div class="form-row">
                    <div class="form-group">
                        <label>Rooms</label>
                        <select>
                            <option>1 Room</option>
                            <option>2 Rooms</option>
                            <option>3 Rooms</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label>Guests</label>
                        <select>
                            <option>1 Guest</option>
                            <option>2 Guests</option>
                            <option>3 Guests</option>
                            <option>4 Guests</option>
                            <option>5+ Guests</option>
                        </select>
                    </div>
                </div>
                <div class="form-group">
                    <label>Budget Range</label>
                    <select>
                        <option>Economy (Under $100/night)</option>
                        <option>Mid-range ($100-$300/night)</option>
                        <option>Luxury ($300+/night)</option>
                    </select>
                </div>
                <button class="search-btn">Search Hotels</button>
                <div class="popular-tags">
                    <span>Popular Cities:</span>
                    <a href="#">New York</a>
                    <a href="#">Paris</a>
                    <a href="#">Tokyo</a>
                    <a href="#">Dubai</a>
                </div>
            </div>
        </div>
    </section>

    <section id="packages" style="background-image: linear-gradient(rgba(255,255,255,0.5), rgba(255,255,255,0.5)), url('https://images.unsplash.com/photo-1508672019048-805c876b67e2?ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80')">
        <h2>Vacation Packages</h2>
        <p>All-inclusive vacation deals that combine flights, hotels, and activities for a hassle-free experience.</p>
    </section>

    <section id="contact" style="background-image: linear-gradient(rgba(255,255,255,0.5), rgba(255,255,255,0.5)), url('https://images.unsplash.com/photo-1526778548025-fa2f459cd5c1?ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80')">
        <h2>Contact Our Travel Experts</h2>
        <p>Have questions? Our 24/7 customer service team is ready to assist you with all your travel needs.</p>
    </section>

    <section id="login" style="background-image: linear-gradient(rgba(255,255,255,0.5), rgba(255,255,255,0.5)), url('https://images.unsplash.com/photo-1505576399279-565b52d4ac71?ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80')">
        <h2>Manage Your Bookings</h2>
        <p>View your upcoming trips, make changes, or check your loyalty points balance.</p>
    </section>

    <footer>
        <div class="footer-content">
            <div class="footer-about">
                <h3>About TravX</h3>
                <p>Founded in 2020, TravX has helped over 1 million travelers book their perfect vacations. Our mission is to make travel planning effortless and affordable for everyone.</p>
            </div>
            <p>&copy; 2025 TravX. All rights reserved.</p>
            <div class="footer-links">
                <a href="#">Terms</a>
                <a href="#">Privacy</a>
                <a href="#">Contact</a>
            </div>
        </div>
    </footer>

    <script>
        // Optimized scroll handler with debounce
        let lastScroll = 0;
        function handleScroll() {
            const scrollPosition = window.pageYOffset;
            if (Math.abs(scrollPosition - lastScroll) > 10) { // Throttle updates
                lastScroll = scrollPosition;
                const parallaxSections = document.querySelectorAll('section');
                requestAnimationFrame(() => {
                    parallaxSections.forEach(section => {
                        const speed = section.getAttribute('data-speed') || 0.3; // Slower parallax
                        section.style.backgroundPositionY = `${scrollPosition * speed}px`;
                    });
                });
            }
        }
        window.addEventListener('scroll', handleScroll, { passive: true });

        // Background transition effect
        let currentSection = 0;
        const sections = document.querySelectorAll('section');
        const colors = ['#1a365d', '#2c3e50', '#4a5568', '#2d3748'];
        
        window.addEventListener('scroll', function() {
            const scrollPosition = window.scrollY;
            const windowHeight = window.innerHeight;
            currentSection = Math.floor(scrollPosition / windowHeight);
            
            if (currentSection < sections.length) {
                document.body.style.backgroundColor = colors[currentSection] || '#f8f9fa';
            }
            
            // Fade in/out effect
            sections.forEach((section, index) => {
                const opacity = 1 - Math.abs(scrollPosition/windowHeight - index) * 0.8;
                section.style.opacity = Math.max(0, Math.min(1, opacity));
            });
        });

        // Enhanced Intersection Observer with momentum scrolling
        const observer = new IntersectionObserver((entries) => {
            requestAnimationFrame(() => {
                entries.forEach(entry => {
                    if (entry.isIntersecting) {
                        entry.target.classList.add('in-view');
                        entry.target.style.transform = 'translateY(0)';
                        entry.target.style.opacity = '1';
                    } else {
                        entry.target.classList.remove('in-view');
                    }
                });
            });
        }, { 
            threshold: 0.2, /* Lower threshold for faster response */
            rootMargin: '100px 0px' /* Smaller root margin */
        });

        document.querySelectorAll('section').forEach(section => {
            observer.observe(section);
        });

        // Navbar scroll effect
        window.addEventListener('scroll', () => {
            const navbar = document.getElementById('navbar');
            navbar.classList.toggle('scrolled', window.scrollY > 50);
        });

        // Mobile menu toggle
        const hamburger = document.querySelector('.hamburger');
        const navLinks = document.querySelector('.nav-links');
        const navItems = document.querySelectorAll('.nav-links li');

        hamburger.addEventListener('click', () => {
            navLinks.classList.toggle('open');
            
            // Animate links
            navItems.forEach((link, index) => {
                if (link.style.animation) {
                    link.style.animation = '';
                } else {
                    link.style.animation = `navItemFade 0.5s ease forwards ${index / 7 + 0.3}s`;
                }
            });
            
            // Hamburger animation
            hamburger.classList.toggle('toggle');
        });

        // Close mobile menu when clicking a nav item
        navItems.forEach(item => {
            item.addEventListener('click', () => {
                if (window.innerWidth <= 768) {
                    navLinks.classList.remove('open');
                    hamburger.classList.remove('toggle');
                    navItems.forEach(link => {
                        link.style.animation = '';
                    });
                }
            });
        });

        // Enhanced smooth scrolling
        document.querySelectorAll('a[href^="#"]').forEach(anchor => {
            anchor.addEventListener('click', function(e) {
                e.preventDefault();
                const targetId = this.getAttribute('href');
                const targetElement = document.querySelector(targetId);
                
                const options = {
                    behavior: 'smooth',
                    block: 'start',
                    inline: 'nearest'
                };
                
                // Scroll slightly above target for better visibility
                const topOffset = window.innerWidth <= 768 ? 60 : 80;
                const elementPosition = targetElement.getBoundingClientRect().top;
                const offsetPosition = elementPosition + window.pageYOffset - topOffset;

                window.scrollTo({
                    top: offsetPosition,
                    ...options
                });

                // Focus target to improve accessibility 
                targetElement.setAttribute('tabindex', '-1');
                targetElement.focus();
            });
        });

        // Interactive buttons
        document.querySelectorAll('.cta-btn, .task-btn').forEach(btn => {
            btn.addEventListener('click', function() {
                this.classList.add('clicked');
                setTimeout(() => {
                    this.classList.remove('clicked');
                }, 300);
                // For demo purposes
                console.log(`${this.textContent} clicked`);
            });
        });

        // Form validation would go here
    </script>
</body>
</html>
