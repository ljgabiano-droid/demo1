<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Lumina | Creative Blog & Portfolio</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://unpkg.com/lucide@latest"></script>
    <link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@300;400;500;600;700&family=Inter:wght@300;400;500;600&display=swap" rel="stylesheet">
    <style>
        * {
            font-family: 'Inter', sans-serif;
        }
        h1, h2, h3, h4, h5, h6 {
            font-family: 'Space Grotesk', sans-serif;
        }
        
        /* Custom Scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-track {
            background: rgba(0,0,0,0.05);
        }
        ::-webkit-scrollbar-thumb {
            background: rgba(0,0,0,0.2);
            border-radius: 4px;
        }
        
        /* Animations */
        @keyframes float {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-20px); }
        }
        @keyframes float-delayed {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-20px); }
        }
        .animate-float {
            animation: float 6s ease-in-out infinite;
        }
        .animate-float-delayed {
            animation: float-delayed 6s ease-in-out infinite;
            animation-delay: 3s;
        }
        
        /* Glassmorphism */
        .glass {
            background: rgba(255, 255, 255, 0.7);
            backdrop-filter: blur(20px);
            -webkit-backdrop-filter: blur(20px);
            border: 1px solid rgba(255, 255, 255, 0.3);
        }
        .glass-dark {
            background: rgba(17, 24, 39, 0.7);
            backdrop-filter: blur(20px);
            -webkit-backdrop-filter: blur(20px);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        /* Gradient Text */
        .gradient-text {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }
        
        /* Page Transitions */
        .page-section {
            display: none;
            opacity: 0;
            transition: opacity 0.4s ease-in-out;
        }
        .page-section.active {
            display: block;
            opacity: 1;
        }
        
        /* Card Hover Effects */
        .blog-card {
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
        }
        .blog-card:hover {
            transform: translateY(-8px);
            box-shadow: 0 20px 40px -15px rgba(0, 0, 0, 0.2);
        }
        
        /* Loading Animation */
        .loader {
            border-top-color: #667eea;
            -webkit-animation: spinner 1.5s linear infinite;
            animation: spinner 1.5s linear infinite;
        }
        @keyframes spinner {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        
        /* Cursor Effect */
        .cursor-dot,
        .cursor-outline {
            position: fixed;
            top: 0;
            left: 0;
            transform: translate(-50%, -50%);
            border-radius: 50%;
            z-index: 9999;
            pointer-events: none;
        }
        .cursor-dot {
            width: 5px;
            height: 5px;
            background-color: #667eea;
        }
        .cursor-outline {
            width: 30px;
            height: 30px;
            border: 2px solid rgba(102, 126, 234, 0.5);
            transition: width 0.2s, height 0.2s, background-color 0.2s;
        }
    </style>
</head>
<body class="bg-gray-50 text-gray-900 overflow-x-hidden transition-colors duration-300" id="body">

    <!-- Custom Cursor -->
    <div class="cursor-dot hidden md:block"></div>
    <div class="cursor-outline hidden md:block"></div>

    <!-- Navigation -->
    <nav class="fixed w-full z-50 transition-all duration-300" id="navbar">
        <div class="glass mx-4 mt-4 rounded-2xl px-6 py-4 max-w-7xl mx-auto">
            <div class="flex justify-between items-center">
                <div class="flex items-center space-x-2 cursor-pointer" onclick="router.navigate('home')">
                    <div class="w-10 h-10 bg-gradient-to-br from-indigo-500 to-purple-600 rounded-xl flex items-center justify-center text-white font-bold text-xl">
                        L
                    </div>
                    <span class="text-xl font-bold tracking-tight">Lumina</span>
                </div>
                
                <div class="hidden md:flex items-center space-x-8">
                    <button onclick="router.navigate('home')" class="nav-link text-sm font-medium hover:text-indigo-600 transition-colors relative group">
                        Home
                        <span class="absolute -bottom-1 left-0 w-0 h-0.5 bg-indigo-600 transition-all group-hover:w-full"></span>
                    </button>
                    <button onclick="router.navigate('blog')" class="nav-link text-sm font-medium hover:text-indigo-600 transition-colors relative group">
                        Blog
                        <span class="absolute -bottom-1 left-0 w-0 h-0.5 bg-indigo-600 transition-all group-hover:w-full"></span>
                    </button>
                    <button onclick="router.navigate('about')" class="nav-link text-sm font-medium hover:text-indigo-600 transition-colors relative group">
                        About
                        <span class="absolute -bottom-1 left-0 w-0 h-0.5 bg-indigo-600 transition-all group-hover:w-full"></span>
                    </button>
                    <button onclick="router.navigate('contact')" class="nav-link text-sm font-medium hover:text-indigo-600 transition-colors relative group">
                        Contact
                        <span class="absolute -bottom-1 left-0 w-0 h-0.5 bg-indigo-600 transition-all group-hover:w-full"></span>
                    </button>
                </div>

                <div class="flex items-center space-x-4">
                    <button onclick="theme.toggle()" class="p-2 rounded-full hover:bg-gray-200 transition-colors">
                        <i data-lucide="sun" class="w-5 h-5 hidden dark:hidden" id="sun-icon"></i>
                        <i data-lucide="moon" class="w-5 h-5 hidden" id="moon-icon"></i>
                    </button>
                    <button class="md:hidden p-2" onclick="mobileMenu.toggle()">
                        <i data-lucide="menu" class="w-6 h-6"></i>
                    </button>
                </div>
            </div>
        </div>
    </nav>

    <!-- Mobile Menu -->
    <div id="mobile-menu" class="fixed inset-0 z-40 hidden">
        <div class="absolute inset-0 bg-black/50 backdrop-blur-sm" onclick="mobileMenu.close()"></div>
        <div class="absolute right-0 top-0 h-full w-64 glass p-8 transform translate-x-full transition-transform duration-300" id="mobile-menu-panel">
            <button onclick="mobileMenu.close()" class="absolute top-4 right-4">
                <i data-lucide="x" class="w-6 h-6"></i>
            </button>
            <div class="mt-12 flex flex-col space-y-6">
                <button onclick="router.navigate('home'); mobileMenu.close()" class="text-left text-lg font-medium">Home</button>
                <button onclick="router.navigate('blog'); mobileMenu.close()" class="text-left text-lg font-medium">Blog</button>
                <button onclick="router.navigate('about'); mobileMenu.close()" class="text-left text-lg font-medium">About</button>
                <button onclick="router.navigate('contact'); mobileMenu.close()" class="text-left text-lg font-medium">Contact</button>
            </div>
        </div>
    </div>

    <!-- Main Content -->
    <main class="pt-24 pb-12 px-4 max-w-7xl mx-auto min-h-screen">
        
        <!-- Home Section -->
        <section id="home" class="page-section active">
            <!-- Hero -->
            <div class="relative overflow-hidden rounded-3xl bg-gradient-to-br from-indigo-600 via-purple-600 to-pink-500 text-white p-8 md:p-16 mb-12">
                <div class="absolute inset-0 overflow-hidden">
                    <div class="absolute -top-24 -right-24 w-96 h-96 bg-white/10 rounded-full blur-3xl animate-float"></div>
                    <div class="absolute -bottom-24 -left-24 w-96 h-96 bg-purple-500/30 rounded-full blur-3xl animate-float-delayed"></div>
                </div>
                <div class="relative z-10 max-w-3xl">
                    <h1 class="text-5xl md:text-7xl font-bold mb-6 leading-tight">
                        Ideas that <span class="text-transparent bg-clip-text bg-gradient-to-r from-yellow-300 to-pink-300">ignite</span> change
                    </h1>
                    <p class="text-xl md:text-2xl text-indigo-100 mb-8 leading-relaxed">
                        Exploring the intersection of design, technology, and human creativity. Join me on a journey through code, art, and innovation.
                    </p>
                    <div class="flex flex-wrap gap-4">
                        <button onclick="router.navigate('blog')" class="px-8 py-4 bg-white text-indigo-600 rounded-full font-semibold hover:shadow-xl hover:scale-105 transition-all flex items-center gap-2">
                            Read Blog <i data-lucide="arrow-right" class="w-5 h-5"></i>
                        </button>
                        <button onclick="router.navigate('about')" class="px-8 py-4 bg-white/10 backdrop-blur border border-white/30 rounded-full font-semibold hover:bg-white/20 transition-all">
                            Learn More
                        </button>
                    </div>
                </div>
            </div>

            <!-- Featured Posts -->
            <div class="mb-12">
                <div class="flex justify-between items-end mb-8">
                    <div>
                        <h2 class="text-3xl font-bold mb-2">Featured Stories</h2>
                        <p class="text-gray-600">Curated thoughts on design and development</p>
                    </div>
                    <button onclick="router.navigate('blog')" class="hidden md:flex items-center gap-2 text-indigo-600 font-medium hover:gap-3 transition-all">
                        View All <i data-lucide="arrow-right" class="w-4 h-4"></i>
                    </button>
                </div>
                
                <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-6" id="featured-posts">
                    <!-- Posts injected by JS -->
                </div>
            </div>

            <!-- Newsletter -->
            <div class="glass rounded-3xl p-8 md:p-12 text-center relative overflow-hidden">
                <div class="absolute top-0 left-0 w-full h-2 bg-gradient-to-r from-indigo-500 via-purple-500 to-pink-500"></div>
                <h3 class="text-2xl md:text-3xl font-bold mb-4">Stay in the loop</h3>
                <p class="text-gray-600 mb-6 max-w-2xl mx-auto">Get the latest articles, tutorials, and insights delivered straight to your inbox. No spam, just quality content.</p>
                <form onsubmit="newsletter.submit(event)" class="flex flex-col sm:flex-row gap-4 max-w-md mx-auto">
                    <input type="email" placeholder="Enter your email" required class="flex-1 px-6 py-3 rounded-full border border-gray-300 focus:outline-none focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200 transition-all">
                    <button type="submit" class="px-8 py-3 bg-gradient-to-r from-indigo-600 to-purple-600 text-white rounded-full font-semibold hover:shadow-lg hover:scale-105 transition-all">
                        Subscribe
                    </button>
                </form>
            </div>
        </section>

        <!-- Blog Section -->
        <section id="blog" class="page-section">
            <div class="mb-8">
                <h2 class="text-4xl font-bold mb-4">All Articles</h2>
                <div class="flex flex-wrap gap-2" id="category-filters">
                    <button onclick="blog.filter('all')" class="px-4 py-2 rounded-full bg-indigo-600 text-white text-sm font-medium transition-all filter-btn active" data-category="all">All</button>
                    <button onclick="blog.filter('design')" class="px-4 py-2 rounded-full bg-gray-200 text-gray-700 hover:bg-gray-300 text-sm font-medium transition-all filter-btn" data-category="design">Design</button>
                    <button onclick="blog.filter('technology')" class="px-4 py-2 rounded-full bg-gray-200 text-gray-700 hover:bg-gray-300 text-sm font-medium transition-all filter-btn" data-category="technology">Technology</button>
                    <button onclick="blog.filter('creativity')" class="px-4 py-2 rounded-full bg-gray-200 text-gray-700 hover:bg-gray-300 text-sm font-medium transition-all filter-btn" data-category="creativity">Creativity</button>
                </div>
            </div>
            
            <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-6" id="blog-grid">
                <!-- All posts injected here -->
            </div>
        </section>

        <!-- Single Post Section -->
        <section id="post" class="page-section">
            <button onclick="router.back()" class="mb-6 flex items-center gap-2 text-gray-600 hover:text-indigo-600 transition-colors">
                <i data-lucide="arrow-left" class="w-4 h-4"></i> Back to articles
            </button>
            <article id="post-content" class="max-w-4xl mx-auto">
                <!-- Post content injected here -->
            </article>
        </section>

        <!-- About Section -->
        <section id="about" class="page-section">
            <div class="grid md:grid-cols-2 gap-12 items-center mb-16">
                <div class="relative">
                    <div class="aspect-square rounded-3xl overflow-hidden bg-gradient-to-br from-indigo-100 to-purple-100 relative">
                        <img src="https://images.unsplash.com/photo-1507003211169-0a1dd7228f2d?w=800&h=800&fit=crop" alt="Profile" class="w-full h-full object-cover hover:scale-110 transition-transform duration-700">
                        <div class="absolute inset-0 bg-gradient-to-t from-indigo-900/20 to-transparent"></div>
                    </div>
                    <div class="absolute -bottom-6 -right-6 w-32 h-32 bg-yellow-400 rounded-2xl rotate-12 opacity-80 blur-sm"></div>
                    <div class="absolute -top-6 -left-6 w-24 h-24 bg-pink-400 rounded-full opacity-60 blur-sm"></div>
                </div>
                <div>
                    <h2 class="text-4xl md:text-5xl font-bold mb-6">Hi, I'm <span class="gradient-text">Alex Chen</span></h2>
                    <p class="text-lg text-gray-600 mb-6 leading-relaxed">
                        I'm a multidisciplinary designer and developer based in San Francisco. With over 8 years of experience in digital product design, I help startups and established companies create meaningful digital experiences.
                    </p>
                    <p class="text-lg text-gray-600 mb-8 leading-relaxed">
                        When I'm not pushing pixels or writing code, you'll find me exploring hiking trails, experimenting with film photography, or brewing the perfect cup of coffee.
                    </p>
                    <div class="flex gap-4">
                        <a href="#" class="p-3 rounded-full bg-gray-100 hover:bg-indigo-100 hover:text-indigo-600 transition-all">
                            <i data-lucide="twitter" class="w-5 h-5"></i>
                        </a>
                        <a href="#" class="p-3 rounded-full bg-gray-100 hover:bg-indigo-100 hover:text-indigo-600 transition-all">
                            <i data-lucide="github" class="w-5 h-5"></i>
                        </a>
                        <a href="#" class="p-3 rounded-full bg-gray-100 hover:bg-indigo-100 hover:text-indigo-600 transition-all">
                            <i data-lucide="linkedin" class="w-5 h-5"></i>
                        </a>
                        <a href="#" class="p-3 rounded-full bg-gray-100 hover:bg-indigo-100 hover:text-indigo-600 transition-all">
                            <i data-lucide="instagram" class="w-5 h-5"></i>
                        </a>
                    </div>
                </div>
            </div>

            <!-- Skills -->
            <div class="mb-16">
                <h3 class="text-2xl font-bold mb-8 text-center">Skills & Expertise</h3>
                <div class="grid grid-cols-2 md:grid-cols-4 gap-6">
                    <div class="glass p-6 rounded-2xl text-center hover:scale-105 transition-transform cursor-pointer group">
                        <div class="w-12 h-12 mx-auto mb-3 bg-indigo-100 rounded-xl flex items-center justify-center group-hover:bg-indigo-600 transition-colors">
                            <i data-lucide="palette" class="w-6 h-6 text-indigo-600 group-hover:text-white transition-colors"></i>
                        </div>
                        <h4 class="font-semibold">UI/UX Design</h4>
                    </div>
                    <div class="glass p-6 rounded-2xl text-center hover:scale-105 transition-transform cursor-pointer group">
                        <div class="w-12 h-12 mx-auto mb-3 bg-purple-100 rounded-xl flex items-center justify-center group-hover:bg-purple-600 transition-colors">
                            <i data-lucide="code" class="w-6 h-6 text-purple-600 group-hover:text-white transition-colors"></i>
                        </div>
                        <h4 class="font-semibold">Frontend Dev</h4>
                    </div>
                    <div class="glass p-6 rounded-2xl text-center hover:scale-105 transition-transform cursor-pointer group">
                        <div class="w-12 h-12 mx-auto mb-3 bg-pink-100 rounded-xl flex items-center justify-center group-hover:bg-pink-600 transition-colors">
                            <i data-lucide="smartphone" class="w-6 h-6 text-pink-600 group-hover:text-white transition-colors"></i>
                        </div>
                        <h4 class="font-semibold">Mobile Design</h4>
                    </div>
                    <div class="glass p-6 rounded-2xl text-center hover:scale-105 transition-transform cursor-pointer group">
                        <div class="w-12 h-12 mx-auto mb-3 bg-yellow-100 rounded-xl flex items-center justify-center group-hover:bg-yellow-600 transition-colors">
                            <i data-lucide="camera" class="w-6 h-6 text-yellow-600 group-hover:text-white transition-colors"></i>
                        </div>
                        <h4 class="font-semibold">Photography</h4>
                    </div>
                </div>
            </div>

            <!-- Timeline -->
            <div class="max-w-3xl mx-auto">
                <h3 class="text-2xl font-bold mb-8 text-center">Journey</h3>
                <div class="space-y-8 relative before:absolute before:inset-0 before:ml-5 before:-translate-x-px md:before:mx-auto md:before:translate-x-0 before:h-full before:w-0.5 before:bg-gradient-to-b before:from-transparent before:via-gray-300 before:to-transparent">
                    <div class="relative flex items-center justify-between md:justify-normal md:odd:flex-row-reverse group is-active">
                        <div class="flex items-center justify-center w-10 h-10 rounded-full border border-white bg-indigo-600 text-white shadow shrink-0 md:order-1 md:group-odd:-translate-x-1/2 md:group-even:translate-x-1/2">
                            <i data-lucide="briefcase" class="w-5 h-5"></i>
                        </div>
                        <div class="w-[calc(100%-4rem)] md:w-[calc(50%-2.5rem)] glass p-6 rounded-2xl">
                            <div class="flex items-center justify-between space-x-2 mb-1">
                                <div class="font-bold text-indigo-600">Senior Designer</div>
                                <time class="font-caveat font-medium text-gray-500 text-sm">2021 - Present</time>
                            </div>
                            <div class="text-gray-900 font-bold mb-2">Stripe</div>
                            <div class="text-gray-600">Leading design systems and product design for payment infrastructure.</div>
                        </div>
                    </div>
                    <div class="relative flex items-center justify-between md:justify-normal md:odd:flex-row-reverse group">
                        <div class="flex items-center justify-center w-10 h-10 rounded-full border border-white bg-white text-gray-600 shadow shrink-0 md:order-1 md:group-odd:-translate-x-1/2 md:group-even:translate-x-1/2">
                            <i data-lucide="briefcase" class="w-5 h-5"></i>
                        </div>
                        <div class="w-[calc(100%-4rem)] md:w-[calc(50%-2.5rem)] glass p-6 rounded-2xl">
                            <div class="flex items-center justify-between space-x-2 mb-1">
                                <div class="font-bold text-indigo-600">Product Designer</div>
                                <time class="font-caveat font-medium text-gray-500 text-sm">2018 - 2021</time>
                            </div>
                            <div class="text-gray-900 font-bold mb-2">Airbnb</div>
                            <div class="text-gray-600">Designed host tools and guest experiences for the platform.</div>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- Contact Section -->
        <section id="contact" class="page-section">
            <div class="max-w-4xl mx-auto">
                <div class="text-center mb-12">
                    <h2 class="text-4xl font-bold mb-4">Let's Create Together</h2>
                    <p class="text-gray-600 text-lg">Have a project in mind or just want to say hi? I'd love to hear from you.</p>
                </div>

                <div class="grid md:grid-cols-2 gap-12">
                    <div class="space-y-6">
                        <div class="glass p-6 rounded-2xl flex items-start gap-4">
                            <div class="w-12 h-12 bg-indigo-100 rounded-xl flex items-center justify-center shrink-0">
                                <i data-lucide="mail" class="w-6 h-6 text-indigo-600"></i>
                            </div>
                            <div>
                                <h4 class="font-bold mb-1">Email</h4>
                                <p class="text-gray-600">hello@lumina.blog</p>
                                <p class="text-sm text-gray-500 mt-1">I usually respond within 24 hours</p>
                            </div>
                        </div>
                        <div class="glass p-6 rounded-2xl flex items-start gap-4">
                            <div class="w-12 h-12 bg-purple-100 rounded-xl flex items-center justify-center shrink-0">
                                <i data-lucide="map-pin" class="w-6 h-6 text-purple-600"></i>
                            </div>
                            <div>
                                <h4 class="font-bold mb-1">Location</h4>
                                <p class="text-gray-600">San Francisco, CA</p>
                                <p class="text-sm text-gray-500 mt-1">Available for remote work worldwide</p>
                            </div>
                        </div>
                        <div class="glass p-6 rounded-2xl flex items-start gap-4">
                            <div class="w-12 h-12 bg-pink-100 rounded-xl flex items-center justify-center shrink-0">
                                <i data-lucide="calendar" class="w-6 h-6 text-pink-600"></i>
                            </div>
                            <div>
                                <h4 class="font-bold mb-1">Schedule a Call</h4>
                                <p class="text-gray-600">Book a 30-min intro call</p>
                                <button class="text-indigo-600 font-medium mt-2 hover:underline">View Calendar →</button>
                            </div>
                        </div>
                    </div>

                    <form onsubmit="contact.submit(event)" class="glass p-8 rounded-3xl space-y-6">
                        <div>
                            <label class="block text-sm font-medium mb-2">Name</label>
                            <input type="text" required class="w-full px-4 py-3 rounded-xl border border-gray-300 focus:outline-none focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200 transition-all bg-white/50">
                        </div>
                        <div>
                            <label class="block text-sm font-medium mb-2">Email</label>
                            <input type="email" required class="w-full px-4 py-3 rounded-xl border border-gray-300 focus:outline-none focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200 transition-all bg-white/50">
                        </div>
                        <div>
                            <label class="block text-sm font-medium mb-2">Message</label>
                            <textarea rows="4" required class="w-full px-4 py-3 rounded-xl border border-gray-300 focus:outline-none focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200 transition-all bg-white/50 resize-none"></textarea>
                        </div>
                        <button type="submit" class="w-full py-4 bg-gradient-to-r from-indigo-600 to-purple-600 text-white rounded-xl font-semibold hover:shadow-lg hover:scale-[1.02] transition-all flex items-center justify-center gap-2">
                            Send Message <i data-lucide="send" class="w-4 h-4"></i>
                        </button>
                    </form>
                </div>
            </div>
        </section>

    </main>

    <!-- Footer -->
    <footer class="border-t border-gray-200 mt-12 py-12 px-4">
        <div class="max-w-7xl mx-auto flex flex-col md:flex-row justify-between items-center gap-6">
            <div class="flex items-center gap-2">
                <div class="w-8 h-8 bg-gradient-to-br from-indigo-500 to-purple-600 rounded-lg flex items-center justify-center text-white font-bold">L</div>
                <span class="font-bold text-lg">Lumina</span>
            </div>
            <p class="text-gray-500 text-sm">© 2026 Lumina Blog. Crafted with passion.</p>
            <div class="flex gap-6">
                <a href="#" class="text-gray-400 hover:text-indigo-600 transition-colors"><i data-lucide="twitter" class="w-5 h-5"></i></a>
                <a href="#" class="text-gray-400 hover:text-indigo-600 transition-colors"><i data-lucide="github" class="w-5 h-5"></i></a>
                <a href="#" class="text-gray-400 hover:text-indigo-600 transition-colors"><i data-lucide="linkedin" class="w-5 h-5"></i></a>
            </div>
        </div>
    </footer>

    <!-- Toast Notification -->
    <div id="toast" class="fixed bottom-8 right-8 transform translate-y-20 opacity-0 transition-all duration-300 z-50">
        <div class="glass-dark text-white px-6 py-4 rounded-2xl shadow-2xl flex items-center gap-3">
            <i data-lucide="check-circle" class="w-5 h-5 text-green-400"></i>
            <span id="toast-message">Success!</span>
        </div>
    </div>

    <script>
        // Initialize Lucide icons
        lucide.createIcons();

        // Blog Data
        const posts = [
            {
                id: 1,
                title: "The Future of Interface Design",
                excerpt: "Exploring how AI and spatial computing are reshaping the way we interact with digital products.",
                category: "design",
                date: "Feb 20, 2026",
                readTime: "5 min read",
                image: "https://images.unsplash.com/photo-1558655146-9f40138edfeb?w=800&h=600&fit=crop",
                content: `
                    <div class="prose prose-lg max-w-none">
                        <p class="lead text-xl text-gray-600 mb-8">The boundaries between physical and digital are dissolving faster than ever before.</p>
                        
                        <p>As we stand on the precipice of a new era in computing, the way we think about interface design is undergoing a fundamental transformation. The flat screens that have defined our digital lives for decades are giving way to spatial, contextual, and increasingly intelligent interfaces.</p>
                        
                        <h3>The Rise of Spatial Interfaces</h3>
                        <p>With the advent of mixed reality headsets and AR glasses, designers are now working in three dimensions. This isn't just about adding depth to flat designs—it's about rethinking how information exists in space.</p>
                        
                        <blockquote>"The best interface is no interface" has never been more relevant. As technology becomes invisible, our designs must become more human.</blockquote>
                        
                        <h3>AI as a Design Material</h3>
                        <p>Artificial intelligence isn't just a tool for automation; it's becoming a core material in our design palette. From predictive interfaces that anticipate user needs to generative UI that adapts in real-time, AI is enabling experiences that were previously impossible.</p>
                        
                        <p>The challenge for modern designers is to harness these capabilities while maintaining the human touch that makes technology meaningful.</p>
                    </div>
                `
            },
            {
                id: 2,
                title: "Building Design Systems at Scale",
                excerpt: "Lessons learned from creating and maintaining design systems for enterprise products.",
                category: "technology",
                date: "Feb 15, 2026",
                readTime: "8 min read",
                image: "https://images.unsplash.com/photo-1551434678-e076c223a692?w=800&h=600&fit=crop",
                content: `
                    <div class="prose prose-lg max-w-none">
                        <p class="lead text-xl text-gray-600 mb-8">Design systems are living organisms that require care, feeding, and evolution.</p>
                        
                        <p>After three years of leading design system efforts at a major tech company, I've learned that creating the system is only 20% of the work. The other 80% is organizational, political, and cultural.</p>
                        
                        <h3>Start with Principles, Not Components</h3>
                        <p>Too many teams jump straight to building a component library without establishing the underlying principles that guide those components. This leads to inconsistency and technical debt.</p>
                        
                        <h3>Governance is Key</h3>
                        <p>Without clear governance, design systems become graveyards of unused components. Establish a steering committee, contribution guidelines, and a clear deprecation strategy from day one.</p>
                    </div>
                `
            },
            {
                id: 3,
                title: "The Art of Creative Coding",
                excerpt: "How programming can be a medium for artistic expression and creative exploration.",
                category: "creativity",
                date: "Feb 10, 2026",
                readTime: "6 min read",
                image: "https://images.unsplash.com/photo-1550745165-9bc0b252726f?w=800&h=600&fit=crop",
                content: `
                    <div class="prose prose-lg max-w-none">
                        <p class="lead text-xl text-gray-600 mb-8">Code is the brush, the screen is the canvas, and algorithms are the paint.</p>
                        
                        <p>Creative coding sits at the intersection of art and technology, offering a unique way to express ideas that static media cannot capture. Through generative art, interactive installations, and procedural design, we're discovering new aesthetic territories.</p>
                        
                        <h3>Embracing Randomness</h3>
                        <p>Unlike traditional design where control is paramount, creative coding often embraces randomness and emergence. The beauty lies in creating systems that produce unexpected yet coherent results.</p>
                        
                        <h3>Tools of the Trade</h3>
                        <p>From Processing and p5.js to TouchDesigner and openFrameworks, the toolkit for creative coding has never been more accessible. These tools lower the barrier to entry while providing powerful capabilities for expression.</p>
                    </div>
                `
            },
            {
                id: 4,
                title: "Minimalism in Digital Products",
                excerpt: "Why less is still more, and how to achieve meaningful simplicity in complex applications.",
                category: "design",
                date: "Feb 5, 2026",
                readTime: "4 min read",
                image: "https://images.unsplash.com/photo-1494438639946-1ebd1d20bf85?w=800&h=600&fit=crop",
                content: "<p>Content for minimalism article...</p>"
            },
            {
                id: 5,
                title: "WebAssembly: The Future of Web Performance",
                excerpt: "Understanding how WebAssembly is enabling high-performance applications in the browser.",
                category: "technology",
                date: "Jan 28, 2026",
                readTime: "7 min read",
                image: "https://images.unsplash.com/photo-1461749280684-dccba630e2f6?w=800&h=600&fit=crop",
                content: "<p>Content about WebAssembly...</p>"
            },
            {
                id: 6,
                title: "Finding Inspiration in Nature",
                excerpt: "Biomimicry in design and how natural patterns can inform digital interfaces.",
                category: "creativity",
                date: "Jan 20, 2026",
                readTime: "5 min read",
                image: "https://images.unsplash.com/photo-1441974231531-c6227db76b6e?w=800&h=600&fit=crop",
                content: "<p>Content about nature inspiration...</p>"
            }
        ];

        // Router
        const router = {
            currentPage: 'home',
            history: [],
            
            navigate(page, params = {}) {
                this.history.push(this.currentPage);
                this.currentPage = page;
                
                // Hide all sections
                document.querySelectorAll('.page-section').forEach(section => {
                    section.classList.remove('active');
                    setTimeout(() => {
                        if (!section.classList.contains('active')) {
                            section.style.display = 'none';
                        }
                    }, 400);
                });
                
                // Show target section
                const target = document.getElementById(page);
                setTimeout(() => {
                    target.style.display = 'block';
                    setTimeout(() => target.classList.add('active'), 10);
                }, page === 'post' ? 0 : 400);
                
                // Update nav active states
                document.querySelectorAll('.nav-link').forEach(link => {
                    link.classList.remove('text-indigo-600');
                });
                
                // Scroll to top
                window.scrollTo({ top: 0, behavior: 'smooth' });
                
                // Handle specific page logic
                if (page === 'blog') {
                    blog.render();
                } else if (page === 'home') {
                    home.renderFeatured();
                } else if (page === 'post') {
                    blog.renderPost(params.id);
                }
                
                lucide.createIcons();
            },
            
            back() {
                if (this.history.length > 0) {
                    const prev = this.history.pop();
                    this.navigate(prev);
                } else {
                    this.navigate('blog');
                }
            }
        };

        // Home Module
        const home = {
            renderFeatured() {
                const container = document.getElementById('featured-posts');
                const featured = posts.slice(0, 3);
                
                container.innerHTML = featured.map(post => `
                    <article class="blog-card glass rounded-2xl overflow-hidden cursor-pointer group" onclick="router.navigate('post', {id: ${post.id}})">
                        <div class="aspect-video overflow-hidden">
                            <img src="${post.image}" alt="${post.title}" class="w-full h-full object-cover group-hover:scale-110 transition-transform duration-500">
                        </div>
                        <div class="p-6">
                            <div class="flex items-center gap-2 mb-3">
                                <span class="px-3 py-1 bg-indigo-100 text-indigo-700 rounded-full text-xs font-semibold uppercase tracking-wider">${post.category}</span>
                                <span class="text-gray-400 text-sm">${post.readTime}</span>
                            </div>
                            <h3 class="text-xl font-bold mb-2 group-hover:text-indigo-600 transition-colors">${post.title}</h3>
                            <p class="text-gray-600 text-sm line-clamp-2">${post.excerpt}</p>
                        </div>
                    </article>
                `).join('');
            }
        };

        // Blog Module
        const blog = {
            currentFilter: 'all',
            
            render() {
                const container = document.getElementById('blog-grid');
                const filtered = this.currentFilter === 'all' 
                    ? posts 
                    : posts.filter(p => p.category === this.currentFilter);
                
                container.innerHTML = filtered.map(post => `
                    <article class="blog-card glass rounded-2xl overflow-hidden cursor-pointer group" onclick="router.navigate('post', {id: ${post.id}})">
                        <div class="aspect-video overflow-hidden relative">
                            <img src="${post.image}" alt="${post.title}" class="w-full h-full object-cover group-hover:scale-110 transition-transform duration-500">
                            <div class="absolute inset-0 bg-gradient-to-t from-black/50 to-transparent opacity-0 group-hover:opacity-100 transition-opacity"></div>
                        </div>
                        <div class="p-6">
                            <div class="flex items-center justify-between mb-3">
                                <span class="px-3 py-1 bg-indigo-100 text-indigo-700 rounded-full text-xs font-semibold uppercase tracking-wider">${post.category}</span>
                                <span class="text-gray-400 text-sm">${post.date}</span>
                            </div>
                            <h3 class="text-xl font-bold mb-2 group-hover:text-indigo-600 transition-colors line-clamp-2">${post.title}</h3>
                            <p class="text-gray-600 text-sm line-clamp-2 mb-4">${post.excerpt}</p>
                            <div class="flex items-center text-indigo-600 font-medium text-sm group-hover:gap-2 transition-all">
                                Read Article <i data-lucide="arrow-right" class="w-4 h-4 ml-1"></i>
                            </div>
                        </div>
                    </article>
                `).join('');
                
                lucide.createIcons();
            },
            
            filter(category) {
                this.currentFilter = category;
                
                // Update buttons
                document.querySelectorAll('.filter-btn').forEach(btn => {
                    if (btn.dataset.category === category) {
                        btn.classList.add('bg-indigo-600', 'text-white');
                        btn.classList.remove('bg-gray-200', 'text-gray-700');
                    } else {
                        btn.classList.remove('bg-indigo-600', 'text-white');
                        btn.classList.add('bg-gray-200', 'text-gray-700');
                    }
                });
                
                this.render();
            },
            
            renderPost(id) {
                const post = posts.find(p => p.id === id);
                if (!post) return;
                
                const container = document.getElementById('post-content');
                container.innerHTML = `
                    <header class="mb-8">
                        <div class="flex items-center gap-2 mb-4">
                            <span class="px-3 py-1 bg-indigo-100 text-indigo-700 rounded-full text-sm font-semibold">${post.category}</span>
                            <span class="text-gray-500">${post.date} · ${post.readTime}</span>
                        </div>
                        <h1 class="text-4xl md:text-5xl font-bold mb-6 leading-tight">${post.title}</h1>
                        <img src="${post.image}" alt="${post.title}" class="w-full h-[400px] object-cover rounded-3xl mb-8">
                    </header>
                    <div class="prose prose-lg max-w-none text-gray-700 leading-relaxed">
                        ${post.content}
                    </div>
                    <div class="mt-12 pt-8 border-t border-gray-200">
                        <h4 class="font-bold mb-4">Share this article</h4>
                        <div class="flex gap-4">
                            <button onclick="toast.show('Shared to Twitter!')" class="p-3 rounded-full bg-gray-100 hover:bg-blue-100 hover:text-blue-600 transition-all">
                                <i data-lucide="twitter" class="w-5 h-5"></i>
                            </button>
                            <button onclick="toast.show('Shared to LinkedIn!')" class="p-3 rounded-full bg-gray-100 hover:bg-blue-100 hover:text-blue-700 transition-all">
                                <i data-lucide="linkedin" class="w-5 h-5"></i>
                            </button>
                            <button onclick="toast.show('Link copied!')" class="p-3 rounded-full bg-gray-100 hover:bg-gray-200 transition-all">
                                <i data-lucide="link" class="w-5 h-5"></i>
                            </button>
                        </div>
                    </div>
                `;
                lucide.createIcons();
            }
        };

        // Theme Manager
        const theme = {
            dark: false,
            
            toggle() {
                this.dark = !this.dark;
                const body = document.getElementById('body');
                const sun = document.getElementById('sun-icon');
                const moon = document.getElementById('moon-icon');
                
                if (this.dark) {
                    body.classList.add('bg-gray-900', 'text-white');
                    body.classList.remove('bg-gray-50', 'text-gray-900');
                    sun.classList.remove('hidden');
                    moon.classList.add('hidden');
                    document.querySelectorAll('.glass').forEach(el => {
                        el.classList.add('glass-dark');
                        el.classList.remove('glass');
                    });
                } else {
                    body.classList.remove('bg-gray-900', 'text-white');
                    body.classList.add('bg-gray-50', 'text-gray-900');
                    sun.classList.add('hidden');
                    moon.classList.remove('hidden');
                    document.querySelectorAll('.glass-dark').forEach(el => {
                        el.classList.add('glass');
                        el.classList.remove('glass-dark');
                    });
                }
            }
        };

        // Mobile Menu
        const mobileMenu = {
            toggle() {
                const menu = document.getElementById('mobile-menu');
                const panel = document.getElementById('mobile-menu-panel');
                menu.classList.remove('hidden');
                setTimeout(() => {
                    panel.classList.remove('translate-x-full');
                }, 10);
            },
            
            close() {
                const menu = document.getElementById('mobile-menu');
                const panel = document.getElementById('mobile-menu-panel');
                panel.classList.add('translate-x-full');
                setTimeout(() => {
                    menu.classList.add('hidden');
                }, 300);
            }
        };

        // Toast Notification
        const toast = {
            show(message) {
                const toast = document.getElementById('toast');
                const msg = document.getElementById('toast-message');
                msg.textContent = message;
                toast.classList.remove('translate-y-20', 'opacity-0');
                setTimeout(() => {
                    toast.classList.add('translate-y-20', 'opacity-0');
                }, 3000);
            }
        };

        // Newsletter
        const newsletter = {
            submit(e) {
                e.preventDefault();
                toast.show('Thanks for subscribing! 🎉');
                e.target.reset();
            }
        };

        // Contact Form
        const contact = {
            submit(e) {
                e.preventDefault();
                toast.show('Message sent successfully! 📧');
                e.target.reset();
            }
        };

        // Custom Cursor
        const cursor = {
            init() {
                const dot = document.querySelector('.cursor-dot');
                const outline = document.querySelector('.cursor-outline');
                
                window.addEventListener('mousemove', (e) => {
                    const posX = e.clientX;
                    const posY = e.clientY;
                    
                    dot.style.left = `${posX}px`;
                    dot.style.top = `${posY}px`;
                    
                    outline.animate({
                        left: `${posX}px`,
                        top: `${posY}px`
                    }, { duration: 500, fill: "forwards" });
                });
                
                // Hover effects
                document.querySelectorAll('a, button').forEach(el => {
                    el.addEventListener('mouseenter', () => {
                        outline.style.width = '50px';
                        outline.style.height = '50px';
                        outline.style.backgroundColor = 'rgba(102, 126, 234, 0.1)';
                    });
                    el.addEventListener('mouseleave', () => {
                        outline.style.width = '30px';
                        outline.style.height = '30px';
                        outline.style.backgroundColor = 'transparent';
                    });
                });
            }
        };

        // Navbar scroll effect
        window.addEventListener('scroll', () => {
            const nav = document.getElementById('navbar');
            if (window.scrollY > 50) {
                nav.classList.add('shadow-lg');
            } else {
                nav.classList.remove('shadow-lg');
            }
        });

        // Initialize
        document.addEventListener('DOMContentLoaded', () => {
            home.renderFeatured();
            cursor.init();
        });
    </script>
</body>
</html>
