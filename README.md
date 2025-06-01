# mrahmee
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PromptCraft - AI Image Generator</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary: #6e48aa;
            --secondary: #9d50bb;
            --dark: #1a1a2e;
            --light: #f8f9fa;
            --success: #4cc9f0;
            --warning: #f72585;
            --gradient: linear-gradient(135deg, var(--primary), var(--secondary));
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: #f5f5f7;
            color: var(--dark);
            line-height: 1.6;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 20px;
        }

        /* Header Styles */
        header {
            background: var(--gradient);
            color: white;
            padding: 1rem 0;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
            position: sticky;
            top: 0;
            z-index: 100;
        }

        .navbar {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .logo {
            font-size: 1.8rem;
            font-weight: 700;
            display: flex;
            align-items: center;
        }

        .logo i {
            margin-right: 10px;
            color: var(--success);
        }

        .nav-links {
            display: flex;
            list-style: none;
        }

        .nav-links li {
            margin-left: 2rem;
        }

        .nav-links a {
            color: white;
            text-decoration: none;
            font-weight: 500;
            transition: all 0.3s ease;
            padding: 0.5rem 0;
            position: relative;
        }

        .nav-links a:hover {
            color: var(--success);
        }

        .nav-links a::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 0;
            width: 0;
            height: 2px;
            background-color: var(--success);
            transition: width 0.3s ease;
        }

        .nav-links a:hover::after {
            width: 100%;
        }

        .mobile-menu-btn {
            display: none;
            background: none;
            border: none;
            color: white;
            font-size: 1.5rem;
            cursor: pointer;
        }

        /* Hero Section */
        .hero {
            text-align: center;
            padding: 4rem 0 2rem;
        }

        .hero h1 {
            font-size: 3rem;
            margin-bottom: 1rem;
            background: var(--gradient);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
        }

        .hero p {
            font-size: 1.2rem;
            max-width: 700px;
            margin: 0 auto 2rem;
            color: #666;
        }

        /* Generator Section */
        .generator {
            background: white;
            border-radius: 12px;
            padding: 2rem;
            box-shadow: 0 8px 30px rgba(0, 0, 0, 0.05);
            margin-bottom: 3rem;
        }

        .generator h2 {
            margin-bottom: 1.5rem;
            color: var(--primary);
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .generator h2 i {
            color: var(--secondary);
        }

        .input-group {
            display: flex;
            margin-bottom: 1.5rem;
            gap: 10px;
        }

        .input-group input {
            flex: 1;
            padding: 1rem;
            border: 2px solid #eee;
            border-radius: 8px;
            font-size: 1rem;
            transition: all 0.3s ease;
        }

        .input-group input:focus {
            outline: none;
            border-color: var(--primary);
            box-shadow: 0 0 0 3px rgba(110, 72, 170, 0.2);
        }

        .btn {
            padding: 1rem 2rem;
            background: var(--gradient);
            color: white;
            border: none;
            border-radius: 8px;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
        }

        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 20px rgba(110, 72, 170, 0.3);
        }

        .btn:disabled {
            background: #ccc;
            cursor: not-allowed;
            transform: none;
            box-shadow: none;
        }

        .result-container {
            margin-top: 2rem;
            text-align: center;
        }

        .result-image {
            max-width: 100%;
            border-radius: 8px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
            display: none;
        }

        .loading {
            display: none;
            margin: 2rem auto;
            text-align: center;
        }

        .spinner {
            width: 50px;
            height: 50px;
            border: 5px solid rgba(110, 72, 170, 0.2);
            border-radius: 50%;
            border-top-color: var(--primary);
            animation: spin 1s linear infinite;
            margin: 0 auto 1rem;
        }

        @keyframes spin {
            to { transform: rotate(360deg); }
        }

        .error-message {
            color: var(--warning);
            margin-top: 1rem;
            display: none;
        }

        /* Gallery Section */
        .gallery {
            padding: 2rem 0;
        }

        .gallery h2 {
            text-align: center;
            margin-bottom: 2rem;
            color: var(--primary);
        }

        .image-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            gap: 20px;
        }

        .image-card {
            background: white;
            border-radius: 8px;
            overflow: hidden;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
            transition: transform 0.3s ease;
        }

        .image-card:hover {
            transform: translateY(-5px);
        }

        .image-card img {
            width: 100%;
            height: 200px;
            object-fit: cover;
        }

        .image-card p {
            padding: 1rem;
            font-size: 0.9rem;
            color: #555;
        }

        /* Footer */
        footer {
            background: var(--dark);
            color: white;
            padding: 3rem 0 1rem;
            margin-top: 3rem;
        }

        .footer-content {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 2rem;
            margin-bottom: 2rem;
        }

        .footer-column h3 {
            font-size: 1.2rem;
            margin-bottom: 1.5rem;
            position: relative;
            padding-bottom: 10px;
        }

        .footer-column h3::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 0;
            width: 50px;
            height: 2px;
            background: var(--gradient);
        }

        .footer-column ul {
            list-style: none;
        }

        .footer-column ul li {
            margin-bottom: 0.8rem;
        }

        .footer-column ul li a {
            color: #bbb;
            text-decoration: none;
            transition: color 0.3s ease;
        }

        .footer-column ul li a:hover {
            color: var(--success);
        }

        .social-links {
            display: flex;
            gap: 1rem;
            margin-top: 1rem;
        }

        .social-links a {
            color: white;
            background: rgba(255, 255, 255, 0.1);
            width: 40px;
            height: 40px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: all 0.3s ease;
        }

        .social-links a:hover {
            background: var(--gradient);
            transform: translateY(-3px);
        }

        .footer-bottom {
            text-align: center;
            padding-top: 2rem;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
            color: #bbb;
            font-size: 0.9rem;
        }

        /* Responsive Styles */
        @media (max-width: 768px) {
            .nav-links {
                position: fixed;
                top: 70px;
                left: -100%;
                width: 100%;
                height: calc(100vh - 70px);
                background: var(--dark);
                flex-direction: column;
                align-items: center;
                padding-top: 2rem;
                transition: all 0.5s ease;
            }

            .nav-links.active {
                left: 0;
            }

            .nav-links li {
                margin: 1rem 0;
            }

            .mobile-menu-btn {
                display: block;
            }

            .hero h1 {
                font-size: 2.2rem;
            }

            .input-group {
                flex-direction: column;
            }

            .btn {
                width: 100%;
            }
        }
    </style>
</head>
<body>
    <header>
        <div class="container">
            <nav class="navbar">
                <div class="logo">
                    <i class="fas fa-magic"></i>
                    <span>PromptCraft</span>
                </div>
                <button class="mobile-menu-btn" id="mobileMenuBtn">
                    <i class="fas fa-bars"></i>
                </button>
                <ul class="nav-links" id="navLinks">
                    <li><a href="#"><i class="fas fa-home"></i> Home</a></li>
                    <li><a href="#generator"><i class="fas fa-image"></i> Generator</a></li>
                    <li><a href="#gallery"><i class="fas fa-photo-video"></i> Gallery</a></li>
                    <li><a href="#"><i class="fas fa-info-circle"></i> About</a></li>
                </ul>
            </nav>
        </div>
    </header>

    <section class="hero">
        <div class="container">
            <h1>Transform Words into Stunning Visuals</h1>
            <p>Our AI-powered image generator turns your creative prompts into beautiful artwork in seconds. Unleash your imagination!</p>
        </div>
    </section>

    <section class="generator" id="generator">
        <div class="container">
            <h2><i class="fas fa-wand-magic-sparkles"></i> AI Image Generator</h2>
            <div class="input-group">
                <input type="text" id="promptInput" placeholder="Describe the image you want to generate (e.g. 'A futuristic city at sunset')">
                <button id="generateBtn" class="btn"><i class="fas fa-sparkles"></i> Generate</button>
            </div>
            
            <div class="loading" id="loadingIndicator">
                <div class="spinner"></div>
                <p>Generating your image... This may take a moment.</p>
            </div>
            
            <div class="error-message" id="errorMessage"></div>
            
            <div class="result-container">
                <img id="resultImage" class="result-image" alt="Generated image will appear here">
            </div>
        </div>
    </section>

    <section class="gallery" id="gallery">
        <div class="container">
            <h2><i class="fas fa-images"></i> Inspiration Gallery</h2>
            <div class="image-grid">
                <div class="image-card">
                    <img src="https://images.unsplash.com/photo-1682686580391-615b3b0b1aad?q=80&w=1000&auto=format&fit=crop" alt="AI generated image">
                    <p>"A serene lake in the mountains at golden hour"</p>
                </div>
                <div class="image-card">
                    <img src="https://images.unsplash.com/photo-1682695796954-bad0d0f59ff1?q=80&w=1000&auto=format&fit=crop" alt="AI generated image">
                    <p>"Cyberpunk city street with neon lights"</p>
                </div>
                <div class="image-card">
                    <img src="https://images.unsplash.com/photo-1682686580391-615b3b0b1aad?q=80&w=1000&auto=format&fit=crop" alt="AI generated image">
                    <p>"Portrait of a steampunk inventor"</p>
                </div>
                <div class="image-card">
                    <img src="https://images.unsplash.com/photo-1682695796954-bad0d0f59ff1?q=80&w=1000&auto=format&fit=crop" alt="AI generated image">
                    <p>"Magical forest with glowing mushrooms"</p>
                </div>
            </div>
        </div>
    </section>

    <footer>
        <div class="container">
            <div class="footer-content">
                <div class="footer-column">
                    <h3>PromptCraft</h3>
                    <p>Transforming your imagination into visual reality with the power of AI.</p>
                    <div class="social-links">
                        <a href="#"><i class="fab fa-twitter"></i></a>
                        <a href="#"><i class="fab fa-instagram"></i></a>
                        <a href="#"><i class="fab fa-discord"></i></a>
                        <a href="#"><i class="fab fa-github"></i></a>
                    </div>
                </div>
                <div class="footer-column">
                    <h3>Quick Links</h3>
                    <ul>
                        <li><a href="#">Home</a></li>
                        <li><a href="#generator">Generator</a></li>
                        <li><a href="#gallery">Gallery</a></li>
                        <li><a href="#">About Us</a></li>
                    </ul>
                </div>
                <div class="footer-column">
                    <h3>Resources</h3>
                    <ul>
                        <li><a href="#">Prompt Guide</a></li>
                        <li><a href="#">API Documentation</a></li>
                        <li><a href="#">Community</a></li>
                        <li><a href="#">Blog</a></li>
                    </ul>
                </div>
                <div class="footer-column">
                    <h3>Legal</h3>
                    <ul>
                        <li><a href="#">Terms of Service</a></li>
                        <li><a href="#">Privacy Policy</a></li>
                        <li><a href="#">Cookie Policy</a></li>
                        <li><a href="#">Copyright</a></li>
                    </ul>
                </div>
            </div>
            <div class="footer-bottom">
                <p>&copy; 2023 PromptCraft. All rights reserved. Powered by Hugging Face AI.</p>
            </div>
        </div>
    </footer>

    <script>
        // Mobile menu toggle
        const mobileMenuBtn = document.getElementById('mobileMenuBtn');
        const navLinks = document.getElementById('navLinks');

        mobileMenuBtn.addEventListener('click', () => {
            navLinks.classList.toggle('active');
        });

        // Close mobile menu when clicking on a link
        document.querySelectorAll('.nav-links a').forEach(link => {
            link.addEventListener('click', () => {
                navLinks.classList.remove('active');
            });
        });

        // Image generation functionality
        const generateBtn = document.getElementById('generateBtn');
        const promptInput = document.getElementById('promptInput');
        const resultImage = document.getElementById('resultImage');
        const loadingIndicator = document.getElementById('loadingIndicator');
        const errorMessage = document.getElementById('errorMessage');

        // Replace with your actual Hugging Face API token
        const HF_API_TOKEN = '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';
        const MODEL_NAME = 'runwayml/stable-diffusion-v1-5"'; // You can change this to any other model

        generateBtn.addEventListener('click', async () => {
            const prompt = promptInput.value.trim();
            
            if (!prompt) {
                showError('Please enter a prompt');
                return;
            }
            
            // Clear previous results and errors
            resultImage.style.display = 'none';
            errorMessage.style.display = 'none';
            
            // Show loading indicator
            loadingIndicator.style.display = 'block';
            generateBtn.disabled = true;
            
            try {
                // Call Hugging Face API
                const response = await fetch(
                    `https://api-inference.huggingface.co/models/${MODEL_NAME}`,
                    {
                        method: 'POST',
                        headers: {
                            'Authorization': `Bearer ${HF_API_TOKEN}`,
                            'Content-Type': 'application/json'
                        },
                        body: JSON.stringify({
                            inputs: prompt,
                            options: {
                                wait_for_model: true
                            }
                        })
                    }
                );
                
                if (!response.ok) {
                    const errorData = await response.json();
                    throw new Error(errorData.error || 'Failed to generate image');
                }
                
                // Get the image blob
                const imageBlob = await response.blob();
                const imageUrl = URL.createObjectURL(imageBlob);
                
                // Display the generated image
                resultImage.src = imageUrl;
                resultImage.style.display = 'block';
                
            } catch (error) {
                console.error('Error generating image:', error);
                showError(error.message || 'An error occurred while generating the image. Please try again.');
            } finally {
                // Hide loading indicator
                loadingIndicator.style.display = 'none';
                generateBtn.disabled = false;
            }
        });
        
        function showError(message) {
            errorMessage.textContent = message;
            errorMessage.style.display = 'block';
        }

        // Allow generating with Enter key
        promptInput.addEventListener('keypress', (e) => {
            if (e.key === 'Enter') {
                generateBtn.click();
            }
        });
    </script>
</body>
</html>
