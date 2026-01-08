

Here is the complete code.

**Important Note:**
I cannot save the *dynamic images* (currently stored in your browser's **Local Storage**) directly into the HTML code you are about to copy. An HTML file is a static text file; your images are data living in your browser's cache.

However, **the code below includes the "Auto-Save" feature you requested.**
1.  **Auto-Load:** When you open the HTML file in your browser, it automatically looks in Local Storage and loads any images you previously uploaded.
2.  **Auto-Save:** When you upload new images via the "Admin" button, they are automatically saved to Local Storage.

**How to save your progress:**
Just save the HTML file to your computer (Ctrl+S / Cmd+S). Your images will be preserved because they live in your browser, not in the HTML file.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>JT Plumbing | Northwest Arkansas</title>
    <meta name="description" content="Professional plumbing services in NWA. 25+ Years of experience.">

    <!-- Google Fonts: Manrope (Headings) and Inter (Body) -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin="">
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600&amp;family=Manrope:wght@400;600;700;800&amp;display=swap" rel="stylesheet">

    <style>
        /* --- CSS VARIABLES & THEME --- */
        :root {
            /* Palette: Deep Blue, Black, White */
            --primary-blue: #0a2e52; 
            --accent-blue: #0066cc;  
            --text-black: #0f172a;   
            --text-gray: #64748b;    
            --bg-white: #ffffff;
            --bg-light: #f8fafc;     
            --bg-card: #ffffff;
            
            --border-radius: 4px; 
            --shadow-sm: 0 1px 3px rgba(0,0,0,0.1);
            --shadow-lg: 0 10px 30px -5px rgba(0,0,0,0.1);
            --transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
        }

        /* Dark Mode */
        [data-theme="dark"] {
            --primary-blue: #003366;
            --accent-blue: #3399ff;
            --text-black: #f1f5f9;
            --text-gray: #94a3b8;
            --bg-white: #020617;   
            --bg-light: #0f172a;
            --bg-card: #0f172a;
            --shadow-sm: 0 1px 3px rgba(0,0,0,0.5);
            --shadow-lg: 0 10px 30px -5px rgba(0,0,0,0.5);
        }

        /* --- RESET & BASE --- */
        * { margin: 0; padding: 0; box-sizing: border-box; }
        
        html { 
            scroll-behavior: smooth; 
            /* FIX: Ensures content isn't hidden behind the sticky header when clicking links */
            scroll-padding-top: 100px; 
        }

        body {
            font-family: 'Inter', sans-serif;
            background-color: var(--bg-white);
            color: var(--text-black);
            line-height: 1.7;
            overflow-x: hidden;
            transition: background-color 0.3s, color 0.3s;
        }

        h1, h2, h3, h4, .logo {
            font-family: 'Manrope', sans-serif;
            font-weight: 700;
            line-height: 1.1;
            letter-spacing: -0.02em;
        }

        a { text-decoration: none; color: inherit; transition: var(--transition); }
        ul { list-style: none; }
        img { max-width: 100%; display: block; }

        /* --- UTILITIES --- */
        .container {
            width: 90%;
            max-width: 1280px;
            margin: 0 auto;
            padding: 0 20px;
        }

        .btn {
            display: inline-flex;
            align-items: center;
            justify-content: center;
            padding: 16px 32px;
            border-radius: var(--border-radius);
            font-weight: 600;
            font-size: 0.95rem;
            text-transform: uppercase;
            letter-spacing: 0.5px;
            cursor: pointer;
            transition: var(--transition);
            border: none;
        }

        .btn-primary {
            background-color: var(--text-black);
            color: #fff;
        }

        .btn-primary:hover {
            background-color: var(--accent-blue);
            transform: translateY(-2px);
        }

        [data-theme="dark"] .btn-primary {
            background-color: #fff;
            color: #000;
        }
        
        [data-theme="dark"] .btn-primary:hover {
            background-color: var(--accent-blue);
            color: #fff;
        }
        
        .btn-outline {
            background: transparent;
            border: 1px solid var(--text-black);
            color: var(--text-black);
        }

        [data-theme="dark"] .btn-outline {
            border-color: #fff;
            color: #fff;
        }

        .btn-outline:hover {
            background: var(--text-black);
            color: #fff;
        }

        .section-padding { padding: 100px 0; }
        
        /* Scroll Animation Class */
        .reveal {
            opacity: 0;
            transform: translateY(30px);
            transition: all 0.8s ease-out;
        }
        .reveal.active {
            opacity: 1;
            transform: translateY(0);
        }

        /* --- HEADER --- */
        header {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            z-index: 1000;
            transition: var(--transition);
            padding: 20px 0;
        }

        header.scrolled {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            padding: 15px 0;
            box-shadow: var(--shadow-sm);
            border-bottom: 1px solid rgba(0,0,0,0.05);
        }

        [data-theme="dark"] header.scrolled {
            background: rgba(2, 6, 23, 0.95);
            border-bottom: 1px solid rgba(255,255,255,0.05);
        }

        .nav-wrapper {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .logo {
            font-size: 2.5rem; /* ENLARGED LOGO */
            color: var(--text-black);
            font-weight: 800;
            text-transform: uppercase;
            white-space: nowrap;
        }

        .logo span { color: var(--accent-blue); }

        nav ul { display: flex; gap: 40px; }
        nav a {
            font-size: 0.9rem;
            font-weight: 500;
            color: var(--text-black);
            position: relative;
        }
        
        nav a::after {
            content: '';
            position: absolute;
            width: 0;
            height: 2px;
            bottom: -4px;
            left: 0;
            background-color: var(--accent-blue);
            transition: var(--transition);
        }
        
        nav a:hover::after { width: 100%; }

        .header-controls { display: flex; align-items: center; gap: 15px; }

        .control-btn {
            background: none;
            border: none;
            cursor: pointer;
            color: var(--text-black);
            padding: 8px;
            border-radius: 50%;
            transition: background 0.3s;
        }
        
        .control-btn:hover { background: rgba(0,0,0,0.05); }
        [data-theme="dark"] .control-btn:hover { background: rgba(255,255,255,0.1); }
        
        .control-btn svg { width: 20px; height: 20px; fill: currentColor; }

        /* --- ADMIN MODAL --- */
        .modal {
            display: none;
            position: fixed;
            z-index: 2000;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0,0,0,0.8);
            align-items: center;
            justify-content: center;
        }

        .modal-content {
            background-color: var(--bg-card);
            padding: 40px;
            border-radius: var(--border-radius);
            width: 90%;
            max-width: 500px;
            box-shadow: var(--shadow-lg);
            text-align: center;
            position: relative;
        }

        .close-modal {
            position: absolute;
            top: 15px;
            right: 20px;
            font-size: 28px;
            cursor: pointer;
            color: var(--text-gray);
        }

        .close-modal:hover { color: var(--text-black); }

        .upload-area {
            border: 2px dashed var(--text-gray);
            padding: 30px;
            margin: 20px 0;
            border-radius: var(--border-radius);
            cursor: pointer;
        }

        .upload-area:hover { border-color: var(--accent-blue); background: var(--bg-light); }

        /* --- HERO --- */
        .hero {
            height: 100vh;
            min-height: 700px;
            display: flex;
            align-items: center;
            position: relative;
            overflow: hidden;
        }

        .hero-bg {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-image: url('https://images.unsplash.com/photo-1506905925346-21bda4d32df4?q=80&w=1920&auto=format&fit=crop');
            background-size: cover;
            background-position: center;
            z-index: -2;
        }

        .hero-overlay {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, rgba(10,46,82,0.9) 0%, rgba(10,46,82,0.6) 100%);
            z-index: -1;
        }

        [data-theme="dark"] .hero-overlay {
            background: linear-gradient(90deg, rgba(0,0,0,0.95) 0%, rgba(0,0,0,0.7) 100%);
        }

        .hero-content {
            color: #fff;
            max-width: 800px;
        }

        .hero h1 {
            font-size: 4.5rem;
            margin-bottom: 16px;
            line-height: 1;
        }

        .hero p {
            font-size: 1.25rem;
            margin-bottom: 30px;
            opacity: 0.9;
            font-weight: 300;
            max-width: 600px;
        }
        
        .badge-free {
            display: inline-block;
            background-color: var(--accent-blue);
            color: #fff;
            padding: 5px 15px;
            font-size: 0.9rem;
            font-weight: 700;
            text-transform: uppercase;
            border-radius: 50px;
            margin-bottom: 20px;
            letter-spacing: 1px;
        }

        /* --- ABOUT --- */
        .about {
            background-color: var(--bg-white);
        }

        .about-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 80px;
            align-items: center;
        }

        .about-label {
            font-size: 0.85rem;
            text-transform: uppercase;
            letter-spacing: 2px;
            color: var(--accent-blue);
            font-weight: 700;
            margin-bottom: 16px;
            display: block;
        }

        .about h2 {
            font-size: 3rem;
            margin-bottom: 32px;
            color: var(--text-black);
        }

        .about p {
            font-size: 1.1rem;
            color: var(--text-gray);
            margin-bottom: 24px;
        }

        .stat-row {
            display: flex;
            gap: 60px;
            margin-top: 40px;
            padding-top: 40px;
            border-top: 1px solid rgba(0,0,0,0.1);
        }

        [data-theme="dark"] .stat-row { border-color: rgba(255,255,255,0.1); }

        .stat-item h3 {
            font-size: 3.5rem;
            color: var(--accent-blue);
            line-height: 1;
        }
        
        .stat-item span {
            font-size: 0.9rem;
            color: var(--text-gray);
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .about-img-wrapper {
            position: relative;
            background-color: var(--bg-light); /* Added background to fill space since image is hidden */
            border-radius: var(--border-radius);
            min-height: 400px; /* Maintain height even without image */
        }
        
        .about-img {
            width: 100%;
            height: 600px;
            object-fit: cover;
            border-radius: var(--border-radius);
            box-shadow: var(--shadow-lg);
            
            /* FIX: Hiding the broken image element completely */
            display: none; 
        }

        /* --- SERVICES --- */
        .services {
            background-color: var(--bg-light);
        }

        .section-header {
            text-align: center;
            max-width: 700px;
            margin: 0 auto 80px;
        }

        .section-header h2 {
            font-size: 2.5rem;
            color: var(--text-black);
            margin-bottom: 20px;
        }

        .section-header p {
            color: var(--text-gray);
            font-size: 1.2rem;
        }

        .services-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 30px;
        }

        .service-card {
            background: var(--bg-card);
            padding: 40px;
            border-radius: var(--border-radius);
            box-shadow: var(--shadow-sm);
            transition: var(--transition);
            border: 1px solid transparent;
        }

        .service-card:hover {
            transform: translateY(-10px);
            box-shadow: var(--shadow-lg);
            border-color: var(--accent-blue);
        }

        .service-icon {
            width: 60px;
            height: 60px;
            background: rgba(0, 102, 204, 0.1);
            color: var(--accent-blue);
            display: flex;
            align-items: center;
            justify-content: center;
            border-radius: 50%;
            margin-bottom: 30px;
        }
        
        .service-icon svg { width: 30px; height: 30px; fill: currentColor; }

        .service-card h3 {
            font-size: 1.5rem;
            margin-bottom: 16px;
            color: var(--text-black);
        }

        .service-card p {
            color: var(--text-gray);
            font-size: 0.95rem;
        }

        /* --- GALLERY (ADMIN UPLOADS) --- */
        .gallery-section {
            background-color: var(--bg-white);
        }
        
        .gallery-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            gap: 20px;
        }
        
        .gallery-item {
            border-radius: var(--border-radius);
            overflow: hidden;
            box-shadow: var(--shadow-sm);
            aspect-ratio: 1 / 1;
            position: relative;
        }
        
        .gallery-item img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            transition: transform 0.5s ease;
        }
        
        .gallery-item:hover img {
            transform: scale(1.05);
        }

        /* --- AREAS (Full Width Blue) --- */
        .areas-banner {
            background-color: var(--primary-blue);
            color: #fff;
            padding: 80px 0;
            text-align: center;
        }

        .areas-content h2 {
            font-size: 2.5rem;
            margin-bottom: 40px;
            color: #fff;
        }

        .areas-list {
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
            gap: 30px;
        }

        .area-item {
            background: rgba(255,255,255,0.1);
            padding: 15px 30px;
            border-radius: 50px;
            font-family: 'Manrope', sans-serif;
            font-weight: 600;
            font-size: 1.1rem;
            backdrop-filter: blur(5px);
            border: 1px solid rgba(255,255,255,0.2);
            transition: var(--transition);
        }

        .area-item:hover {
            background: #fff;
            color: var(--primary-blue);
            transform: scale(1.05);
        }

        /* --- CONTACT --- */
        .contact {
            background-color: var(--bg-white);
        }

        .contact-container {
            display: grid;
            grid-template-columns: 1fr 1.2fr;
            gap: 80px;
        }

        .contact-info {
            padding-right: 40px;
        }

        .info-block {
            margin-bottom: 40px;
        }

        .info-block h4 {
            font-size: 1.1rem;
            color: var(--text-black);
            margin-bottom: 12px;
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .info-block p {
            color: var(--text-gray);
            padding-left: 36px;
        }

        .hours {
            background: var(--bg-light);
            padding: 30px;
            border-radius: var(--border-radius);
            border-left: 4px solid var(--accent-blue);
        }
        
        .hours-row {
            display: flex;
            justify-content: space-between;
            margin-bottom: 8px;
            font-size: 0.95rem;
            color: var(--text-gray);
        }

        /* Form Styling */
        .form-box {
            background: var(--bg-white);
            padding: 50px;
            border-radius: var(--border-radius);
            box-shadow: var(--shadow-lg);
            border: 1px solid rgba(0,0,0,0.05);
        }
        
        [data-theme="dark"] .form-box { border-color: rgba(255,255,255,0.05); }

        .form-group { margin-bottom: 24px; }

        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-size: 0.9rem;
            font-weight: 600;
            color: var(--text-black);
        }

        .form-control {
            width: 100%;
            padding: 16px;
            border: 1px solid #e2e8f0;
            border-radius: var(--border-radius);
            background: var(--bg-light);
            color: var(--text-black);
            font-family: 'Inter', sans-serif;
            font-size: 1rem;
            transition: var(--transition);
        }

        .form-control:focus {
            outline: none;
            border-color: var(--accent-blue);
            background: var(--bg-white);
        }

        textarea.form-control { resize: vertical; min-height: 150px; }

        /* --- FOOTER --- */
        footer {
            background-color: var(--text-black);
            color: rgba(255,255,255,0.6);
            padding: 60px 0 30px;
            font-size: 0.9rem;
        }

        .footer-content {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding-bottom: 40px;
            border-bottom: 1px solid rgba(255,255,255,0.1);
            margin-bottom: 30px;
        }

        .footer-branding {
            display: flex;
            flex-direction: column;
        }

        .footer-logo {
            color: #fff;
            font-size: 1.5rem;
            font-weight: 700;
        }

        .license-info {
            font-size: 0.85rem;
            color: rgba(255,255,255,0.7);
            margin-top: 5px;
            font-family: 'Inter', sans-serif;
        }

        .socials a {
            color: #fff;
            margin-left: 20px;
            font-weight: 600;
            transition: var(--transition);
        }

        .socials a:hover { color: var(--accent-blue); }

        /* --- NOTIFICATION --- */
        #notification {
            position: fixed;
            bottom: 30px;
            left: 50%;
            transform: translateX(-50%) translateY(100px);
            background-color: var(--primary-blue);
            color: #fff;
            padding: 16px 32px;
            border-radius: 50px;
            box-shadow: var(--shadow-lg);
            z-index: 2000;
            opacity: 0;
            transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            font-weight: 600;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        #notification.show {
            transform: translateX(-50%) translateY(0);
            opacity: 1;
        }

        /* --- RESPONSIVE --- */
        @media (max-width: 992px) {
            .hero h1 { font-size: 3rem; }
            .about-grid, .contact-container { grid-template-columns: 1fr; gap: 50px; }
            .about-img { height: 400px; }
            .header-controls .btn { display: none; } /* Simplified mobile nav for demo */
            .logo { font-size: 1.8rem; }
        }

        @media (max-width: 768px) {
            nav ul { display: none; }
            .hero { min-height: 500px; }
            .hero h1 { font-size: 2.5rem; }
            .stat-row { gap: 30px; }
        }
    </style>
</head>
<body>

    <!-- Header -->
    <header id="header">
        <div class="container nav-wrapper">
            <!-- Logo links back to top -->
            <a href="#" class="logo">JT <span>Plumbing</span></a>
            <nav>
                <ul>
                    <li><a href="#about">About</a></li>
                    <li><a href="#services">Services</a></li>
                    <li><a href="#gallery">Gallery</a></li> <!-- Link to new gallery -->
                    <li><a href="#areas">Service Areas</a></li>
                    <li><a href="#contact">Contact</a></li>
                </ul>
            </nav>
            <div class="header-controls">
                <!-- Admin Photos Button -->
                <button class="control-btn" id="adminPhotosBtn" title="Upload Your Photos">
                    <svg viewBox="0 0 24 24"><path d="M8.5,13.5L11,16.5L14.5,12L19,18H5M21,19V5C21,3.89 20.1,3 19,3H5A2,2 0 0,0 3,5V19A2,2 0 0,0 5,21H19A2,2 0 0,0 21,19Z"></path></svg>
                </button>
                
                <!-- Theme Toggle -->
                <button class="control-btn" id="themeToggle" aria-label="Toggle Dark Mode">
                    <svg id="moonIcon" viewBox="0 0 24 24"><path d="M12,1A11,11,0,1,0,23,12,11,11,0,0,0,12,1Zm0,19a8,8,0,1,1,8-8A8,8,0,0,1,12,20Z"></path></svg>
                    <svg id="sunIcon" style="display:none;" viewBox="0 0 24 24"><path d="M12,7A5,5,0,1,0,17,12A5,5,0,0,0,12,7Zm0,8A3,3,0,1,1,15,12,3,3,0,1,12,15Zm0-14A1,1,0,0,0,11,2V4A1,1,0,0,0,13,4V2A1,1,0,0,0,12,1Zm0,22a1,1,0,0,0-1,1v2a1,1,0,0,0,2,0V24A1,1,0,0,0,12,23ZM22.66,6.34a1,1,0,0,0-1.41,0l-1.42,1.42a1,1,0,1,0,1.42,1.42l1.41-1.42A1,1,0,0,0,22.66,6.34ZM5.17,18.83a1,1,0,0,0-1.42,0L2.34,20.24a1,1,0,1,0,1.42,1.42l1.41-1.42A1,1,0,0,0,5.17,18.83ZM21.25,20.24l-1.41-1.42a1,1,0,1,0-1.42,1.42l1.41,1.42a1,1,0,0,0,1.42-1.42ZM4.17,7.76L5.58,6.34A1,1,0,1,0,4.17,4.93L2.75,6.34A1,1,0,0,0,4.17,7.76ZM23,11H21a1,1,0,0,0,0,2h2a1,1,0,0,0,0-2ZM3,11H1a1,1,0,0,0,0,2H3a1,1,0,0,0,0-2Z"></path></svg>
                </button>
                <a href="#contact" class="btn btn-primary">Connect Now</a>
            </div>
        </div>
    </header>

    <!-- Admin Modal for Photos -->
    <div id="photoModal" class="modal">
        <div class="modal-content">
            <span class="close-modal" id="closeModal">×</span>
            <h2 style="margin-bottom: 10px;">Upload Photos</h2>
            <p style="color: var(--text-gray); margin-bottom: 20px;">Select images from your device to add to gallery. Images are saved to your browser automatically.</p>
            
            <!-- Added 'multiple' attribute to allow uploading several files at once -->
            <input type="file" id="fileInput" accept="image/*" multiple style="display: none;">
            <div class="upload-area" id="dropArea">
                <svg style="width:40px;height:40px;fill:var(--text-gray);margin-bottom:10px;" viewBox="0 0 24 24"><path d="M9,16V10H5L12,3L19,10H15V16H9M5,20V18H19V20H5Z"></path></svg>
                <p>Click to Select Photos (Multiple Allowed)</p>
            </div>
            
            <button id="uploadBtn" class="btn btn-primary" style="width:100%; margin-top:20px;">Upload Images</button>
        </div>
    </div>

    <!-- Hero -->
    <section class="hero">
        <div class="hero-bg"></div>
        <div class="hero-overlay"></div>
        <div class="container">
            <div class="hero-content reveal">
                <div class="badge-free">Free Estimates</div>
                <h1>Innovative Plumbing Solutions</h1>
                <p>25+ plus Years of Experience in the industry. From new builds to emergency repairs, JT Plumbing delivers professional solutions for Fayetteville and beyond.</p>
                <a href="#contact" class="btn btn-primary">Connect Now</a>
            </div>
        </div>
    </section>

    <!-- About -->
    <section id="about" class="section-padding about">
        <div class="container">
            <div class="about-grid">
                <div class="about-text reveal">
                    <span class="about-label">Who We Are</span>
                    <h2>Deep Roots in the Ozarks</h2>
                    <p>With over two decades of experience, we are confident we can meet your needs whatever they may be. We understand the unique plumbing challenges of the region, from the historic homes of Fayetteville to the new developments in Farmington.</p>
                    <p>We believe in honest work, transparent pricing, and showing up when we say we will. Our team is fully licensed and dedicated to maintaining the integrity of your home or business.</p>
                    
                    <div class="stat-row">
                        <div class="stat-item">
                            <h3>25+</h3>
                            <span>Years Experience</span>
                        </div>
                        <div class="stat-item">
                            <h3>100%</h3>
                            <span>Satisfaction</span>
                        </div>
                    </div>
                </div>
                <div class="about-img-wrapper reveal">
                    <!-- Architectural/Plumbing Image - SRC REMOVED -->
                    <img alt="Professional Plumber Working" class="about-img">
                </div>
            </div>
        </div>
    </section>

    <!-- Services -->
    <section id="services" class="section-padding services">
        <div class="container">
            <div class="section-header reveal">
                <h2>Our Expertise</h2>
                <p>We can handle almost all your needs. Comprehensive solutions designed for longevity and efficiency.</p>
            </div>

            <div class="services-grid">
                <!-- Service 1 -->
                <div class="service-card reveal">
                    <div class="service-icon">
                        <svg viewBox="0 0 24 24"><path d="M12,3L2,12H5V20H10V14H14V20H19V12H22L12,3Z"></path></svg>
                    </div>
                    <h3>New Builds</h3>
                    <p>Complete rough-in and finish plumbing for residential new construction. We work seamlessly with builders to ensure code compliance and modern efficiency.</p>
                </div>

                <!-- Service 2 -->
                <div class="service-card reveal">
                    <div class="service-icon">
                        <svg viewBox="0 0 24 24"><path d="M20.71,7.04C21.1,6.65 21.1,6 20.71,5.63L18.37,3.29C18,2.9 17.35,2.9 16.96,3.29L15.12,5.12L18.87,8.87M3,17.25V21H6.75L17.81,9.93L14.06,6.18L3,17.25Z"></path></svg>
                    </div>
                    <h3>Remodels</h3>
                    <p>Modernizing your space? We specialize in bathroom and kitchen renovations, moving lines, and installing luxury fixtures with precision.</p>
                </div>

                <!-- Service 3 -->
                <div class="service-card reveal">
                    <div class="service-icon">
                        <svg viewBox="0 0 24 24"><path d="M13.78 15.3L19.78 21.3L21.89 19.14L15.89 13.14L13.78 15.3M17.5 10.1C17.11 10.1 16.69 10.05 16.36 9.91L4.97 21.25L2.86 19.14L10.27 11.74L8.5 9.96L7.78 10.66L6.33 9.25V12.11L5.63 12.81L2.11 9.25L2.81 8.55H5.62L4.22 7.14L7.78 3.58C8.95 2.41 10.83 2.41 12 3.58L14.13 5.69C15.29 6.86 15.29 8.74 14.13 9.91L13.46 10.58C14.13 10.33 15.13 10.3 16.06 10.75L17.5 10.1Z"></path></svg>
                    </div>
                    <h3>Residential Repair</h3>
                    <p>Leak detection, drain cleaning, and water heater repair. We respond quickly to minimize damage and restore comfort to your home.</p>
                </div>

                <!-- Service 4 -->
                <div class="service-card reveal">
                    <div class="service-icon">
                        <svg viewBox="0 0 24 24"><path d="M12,7V3H2V21H22V7H12M6,19H4V17H6V19M6,15H4V13H6V15M6,11H4V9H6V11M6,7H4V5H6V7M10,19H8V17H10V19M10,15H8V13H10V15M10,11H8V9H10V11M10,7H8V5H10V7M20,19H12V17H20V19M20,15H12V13H20V15M20,11H12V9H20V11M20,7H12V5H20V7Z"></path></svg>
                    </div>
                    <h3>Small Commercial</h3>
                    <p>Reliable plumbing for offices, retail spaces, and small businesses. Keep your operations running smoothly with our maintenance plans.</p>
                </div>
            </div>
        </div>
    </section>

    <!-- New Gallery Section for Admin Uploads -->
    <section id="gallery" class="section-padding gallery-section">
        <div class="container">
            <div class="section-header reveal">
                <h2>Recent Work</h2>
                <p>A gallery of our latest projects and installations.</p>
            </div>
            <!-- Gallery Grid is now EMPTY. Images will be added via Admin Upload tool -->
            <div class="gallery-grid" id="galleryGrid">
                <!-- Use the "Upload Photos" button in the top toolbar to add your own images. -->
            </div>
        </div>
    </section>

    <!-- Areas -->
    <section id="areas" class="areas-banner">
        <div class="container areas-content reveal">
            <h2>Serving Northwest Arkansas</h2>
            <div class="areas-list">
                <div class="area-item">Fayetteville</div>
                <div class="area-item">Prairie Grove</div>
                <div class="area-item">Lincoln</div>
                <div class="area-item">Farmington</div>
                <div class="area-item">Springdale</div>
                <div class="area-item">Elkins</div>
                <div class="area-item">West Fork</div>
            </div>
        </div>
    </section>

    <!-- Contact -->
    <section id="contact" class="section-padding contact">
        <div class="container">
            <div class="contact-container">
                <div class="contact-info reveal">
                    <span class="about-label">Get In Touch</span>
                    <h2>Ready to Connect?</h2>
                    <p style="margin-bottom: 40px; color: var(--text-gray);">Fill out the form or give us a call. We are ready to tackle your plumbing challenges.</p>
                    
                    <div class="info-block">
                        <h4>
                            <svg style="width:20px;height:20px;fill:var(--accent-blue)" viewBox="0 0 24 24"><path d="M6.62 10.79c1.44 2.83 3.76 5.14 6.59 6.59l2.2-2.2c.27-.27.67-.36 1.02-.24 1.12.37 2.33.57 3.57.57.55 0 1 .45 1 1V20c0 .55-.45 1-1 1-9.39 0-17-7.61-17-17 0-.55.45-1 1-1h3.5c.55 0 1 .45 1 1 0 1.25.2 2.45.57 3.57.11.35.03.74-.25 1.02l-2.2 2.2z"></path></svg>
                            Phone
                        </h4>
                        <p>(817) 727-9444</p>
                    </div>
                    
                    <div class="info-block">
                        <h4>
                            <svg style="width:20px;height:20px;fill:var(--accent-blue)" viewBox="0 0 24 24"><path d="M12 2C8.13 2 5 5.13 5 9c0 5.25 7 13 7 13s7-7.75 7-13c0-3.87-3.13-7-7-7zm0 9.5c-1.38 0-2.5-1.12-2.5-2.5s1.12-2.5 2.5-2.5 2.5 1.12 2.5 2.5-1.12 2.5-2.5 2.5z"></path></svg>
                            Service Area
                        </h4>
                        <p>Fayetteville, Prairie Grove, Lincoln, Farmington & Surrounding Areas</p>
                    </div>

                    <div class="hours">
                        <div class="hours-row">
                            <span>Monday - Friday</span>
                            <span style="font-weight:700; color: var(--text-black);">8:00 AM - 5:00 PM</span>
                        </div>
                        <div class="hours-row">
                            <span>Saturday - Sunday</span>
                            <span>Closed</span>
                        </div>
                    </div>
                </div>

                <div class="form-box reveal">
                    <form id="serviceForm">
                        <div class="form-group">
                            <label for="name">Full Name</label>
                            <input type="text" id="name" class="form-control" placeholder="John Doe" required="">
                        </div>
                        <div class="form-group">
                            <label for="email">Email Address</label>
                            <input type="email" id="email" class="form-control" placeholder="john@example.com" required="">
                        </div>
                        <div class="form-group">
                            <label for="service">Service Needed</label>
                            <select id="service" class="form-control">
                                <option value="repair">Residential Repair</option>
                                <option value="newbuild">New Build</option>
                                <option value="remodel">Remodel</option>
                                <option value="commercial">Small Commercial</option>
                            </select>
                        </div>
                        <div class="form-group">
                            <label for="message">Project Details</label>
                            <textarea id="message" class="form-control" placeholder="Tell us about your plumbing needs..."></textarea>
                        </div>
                        <button type="submit" class="btn btn-primary" style="width: 100%;">Connect Now</button>
                    </form>
                </div>
            </div>
        </div>
    </section>

    <!-- Footer -->
    <footer>
        <div class="container">
            <div class="footer-content">
                <div class="footer-branding">
                    <div class="footer-logo">JT Plumbing</div>
                    <div class="license-info">Master Plumber License # MP7385</div>
                </div>
                <div class="socials">
                    <!-- Instagram and LinkedIn removed as requested. Keeping Facebook. -->
                    <a href="#" target="_blank">Facebook</a>
                </div>
            </div>
            <div style="text-align: center; font-size: 0.8rem; opacity: 0.6;">
                &copy; 2023 JT Plumbing. All rights reserved. Serving Northwest Arkansas.
            </div>
        </div>
    </footer>

    <!-- Notification Toast -->
    <div id="notification">
        <svg style="width:20px;height:20px;fill:#fff" viewBox="0 0 24 24"><path d="M9 16.17L4.83 12l-1.42 1.41L9 19 21 7l-1.41-1.41z"></path></svg>
        <span id="notifText">Request Sent Successfully!</span>
    </div>

    <!-- JavaScript -->
    <script>
        // --- Theme Logic ---
        const themeToggle = document.getElementById('themeToggle');
        const sunIcon = document.getElementById('sunIcon');
        const moonIcon = document.getElementById('moonIcon');
        const html = document.documentElement;

        const savedTheme = localStorage.getItem('theme');
        if (savedTheme === 'dark') {
            html.setAttribute('data-theme', 'dark');
            sunIcon.style.display = 'block';
            moonIcon.style.display = 'none';
        }

        themeToggle.addEventListener('click', () => {
            if (html.getAttribute('data-theme') === 'dark') {
                html.removeAttribute('data-theme');
                localStorage.setItem('theme', 'light');
                sunIcon.style.display = 'none';
                moonIcon.style.display = 'block';
            } else {
                html.setAttribute('data-theme', 'dark');
                localStorage.setItem('theme', 'dark');
                sunIcon.style.display = 'block';
                moonIcon.style.display = 'none';
            }
        });

        // --- Scroll Animation (Reveal) ---
        const observer = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    entry.target.classList.add('active');
                }
            });
        }, { threshold: 0.1 });

        document.querySelectorAll('.reveal').forEach(el => observer.observe(el));

        // --- Sticky Header Effect ---
        window.addEventListener('scroll', () => {
            const header = document.getElementById('header');
            if (window.scrollY > 50) {
                header.classList.add('scrolled');
            } else {
                header.classList.remove('scrolled');
            }
        });

        // --- Form Handling ---
        const form = document.getElementById('serviceForm');
        const notification = document.getElementById('notification');
        const notifText = document.getElementById('notifText');

        form.addEventListener('submit', (e) => {
            e.preventDefault();
            
            const btn = form.querySelector('button');
            const originalText = btn.innerText;
            btn.innerText = 'Sending...';
            btn.style.opacity = '0.7';
            
            setTimeout(() => {
                notifText.innerText = "Request Sent Successfully!";
                notification.classList.add('show');
                form.reset();
                btn.innerText = originalText;
                btn.style.opacity = '1';

                setTimeout(() => {
                    notification.classList.remove('show');
                }, 4000);
            }, 1500);
        });

        // --- Admin Photo Upload Logic (Auto-Save to Local Storage) ---
        const adminBtn = document.getElementById('adminPhotosBtn');
        const modal = document.getElementById('photoModal');
        const closeModal = document.getElementById('closeModal');
        const fileInput = document.getElementById('fileInput');
        const dropArea = document.getElementById('dropArea');
        const uploadBtn = document.getElementById('uploadBtn');
        const galleryGrid = document.getElementById('galleryGrid');
        
        // Storage Key
        const STORAGE_KEY = 'jt_plumbing_gallery_images';

        // Function: Load images from Local Storage
        function loadImagesFromStorage() {
            try {
                const storedImages = JSON.parse(localStorage.getItem(STORAGE_KEY) || '[]');
                
                if (storedImages.length > 0) {
                    storedImages.forEach(imgSrc => {
                        const newItem = document.createElement('div');
                        newItem.className = 'gallery-item reveal active'; // active to show immediately
                        
                        const img = document.createElement('img');
                        img.src = imgSrc;
                        img.alt = "Saved Photo";
                        
                        newItem.appendChild(img);
                        galleryGrid.appendChild(newItem);
                    });
                }
            } catch (e) {
                console.warn("Could not load images from storage", e);
            }
        }

        // Execute Load Function immediately when DOM is ready
        document.addEventListener('DOMContentLoaded', loadImagesFromStorage);

        // Open Modal
        adminBtn.addEventListener('click', () => {
            modal.style.display = 'flex';
        });

        // Close Modal
        closeModal.addEventListener('click', () => {
            modal.style.display = 'none';
        });
        
        window.addEventListener('click', (e) => {
            if (e.target == modal) {
                modal.style.display = 'none';
            }
        });

        // Trigger file input
        dropArea.addEventListener('click', () => {
            fileInput.click();
        });

        // Handle File Selection Display
        fileInput.addEventListener('change', (e) => {
            const files = e.target.files;
            if (files.length > 0) {
                dropArea.querySelector('p').innerText = `${files.length} Image(s) Selected`;
                dropArea.style.borderColor = "var(--accent-blue)";
            } else {
                dropArea.querySelector('p').innerText = "Click to Select Photos (Multiple Allowed)";
                dropArea.style.borderColor = "var(--text-gray)";
            }
        });

        // Handle Upload
        uploadBtn.addEventListener('click', () => {
            if (fileInput.files && fileInput.files.length > 0) {
                const files = Array.from(fileInput.files);
                
                // 1. Get current list from storage to append to it
                let storedImages = [];
                try {
                    storedImages = JSON.parse(localStorage.getItem(STORAGE_KEY) || '[]');
                } catch(e) { console.error(e); }

                // 2. Process all files
                files.forEach(file => {
                    const reader = new FileReader();

                    reader.onload = function(e) {
                        const base64Image = e.target.result;
                        
                        // Add to DOM immediately
                        const newItem = document.createElement('div');
                        newItem.className = 'gallery-item reveal active';
                        
                        const img = document.createElement('img');
                        img.src = base64Image;
                        img.alt = "Admin Upload";
                        
                        newItem.appendChild(img);
                        galleryGrid.prepend(newItem);

                        // Add to storage array
                        storedImages.push(base64Image);
                    }

                    reader.readAsDataURL(file);
                });

                // 3. Save updated array back to Local Storage (After reading all files)
                setTimeout(() => {
                    try {
                        localStorage.setItem(STORAGE_KEY, JSON.stringify(storedImages));
                        notifText.innerText = `${files.length} Photo(s) Uploaded & Saved!`;
                    } catch (e) {
                        console.error("Quota Exceeded", e);
                        alert("Storage Quota Exceeded! Images may not be saved after you close the browser. Please compress images.");
                        notifText.innerText = "Uploaded (Storage Error)";
                    }
                    
                    // Reset UI
                    modal.style.display = 'none';
                    fileInput.value = ''; 
                    dropArea.querySelector('p').innerText = "Click to Select Photos (Multiple Allowed)";
                    dropArea.style.borderColor = "var(--text-gray)";
                    
                    notification.classList.add('show');
                    setTimeout(() => {
                        notification.classList.remove('show');
                    }, 4000);
                }, 500);
            } else {
                alert("Please select at least one image file.");
            }
        });
    </script>

</body>
</html>
```
