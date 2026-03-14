<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Danish Murtaza | CAF Study Hub - ICAP Pakistan</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/gsap.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/ScrollTrigger.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&family=Playfair+Display:wght@700&display=swap" rel="stylesheet">
    
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                        serif: ['Playfair Display', 'serif'],
                    },
                    colors: {
                        primary: '#1e3a8a',
                        secondary: '#3b82f6',
                        accent: '#f59e0b',
                        dark: '#0f172a',
                    }
                }
            }
        }
    </script>
    
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: #0f172a;
            color: #e2e8f0;
            font-family: 'Inter', sans-serif;
            overflow-x: hidden;
            cursor: none;
        }

        /* Custom Cursor */
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
            background-color: #3b82f6;
        }

        .cursor-outline {
            width: 30px;
            height: 30px;
            border: 2px solid rgba(59, 130, 246, 0.5);
            transition: width 0.2s, height 0.2s, background-color 0.2s;
        }

        .cursor-outline.hover {
            width: 50px;
            height: 50px;
            background-color: rgba(59, 130, 246, 0.1);
            border-color: #f59e0b;
        }

        /* Glass Morphism */
        .glass {
            background: rgba(255, 255, 255, 0.03);
            backdrop-filter: blur(20px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            box-shadow: 0 8px 32px 0 rgba(0, 0, 0, 0.37);
        }

        .glass-strong {
            background: rgba(15, 23, 42, 0.7);
            backdrop-filter: blur(20px);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }

        /* 3D Card Effects */
        .card-3d {
            transform-style: preserve-3d;
            transform: perspective(1000px);
        }

        .card-3d-content {
            transform: translateZ(20px);
        }

        .card-3d:hover {
            transform: perspective(1000px) rotateX(5deg) rotateY(5deg) translateZ(30px);
        }

        /* Floating Animation */
        @keyframes float {
            0%, 100% { transform: translateY(0px) rotate(0deg); }
            50% { transform: translateY(-20px) rotate(2deg); }
        }

        @keyframes float-reverse {
            0%, 100% { transform: translateY(0px) rotate(0deg); }
            50% { transform: translateY(20px) rotate(-2deg); }
        }

        .floating { animation: float 6s ease-in-out infinite; }
        .floating-reverse { animation: float-reverse 7s ease-in-out infinite; }
        .floating-slow { animation: float 8s ease-in-out infinite; }

        /* Gradient Text */
        .gradient-text {
            background: linear-gradient(135deg, #60a5fa 0%, #3b82f6 50%, #f59e0b 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        /* Animated Gradient Border */
        .gradient-border {
            position: relative;
            background: rgba(15, 23, 42, 0.8);
            border-radius: 16px;
        }

        .gradient-border::before {
            content: '';
            position: absolute;
            inset: -2px;
            border-radius: 18px;
            background: linear-gradient(45deg, #3b82f6, #f59e0b, #60a5fa, #3b82f6);
            background-size: 400% 400%;
            z-index: -1;
            animation: gradient-rotate 3s ease infinite;
        }

        @keyframes gradient-rotate {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        /* Particle Canvas */
        #particles-canvas {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            pointer-events: none;
        }

        /* Scroll Progress */
        .scroll-progress {
            position: fixed;
            top: 0;
            left: 0;
            height: 3px;
            background: linear-gradient(90deg, #3b82f6, #f59e0b);
            z-index: 10000;
            transform-origin: left;
        }

        /* Magnetic Button */
        .magnetic-btn {
            position: relative;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            transition: transform 0.3s cubic-bezier(0.23, 1, 0.32, 1);
        }

        /* Text Scramble Effect */
        .scramble-text {
            display: inline-block;
        }

        /* Parallax Layers */
        .parallax-layer {
            will-change: transform;
        }

        /* Blob Animation */
        @keyframes blob {
            0%, 100% { border-radius: 60% 40% 30% 70% / 60% 30% 70% 40%; }
            50% { border-radius: 30% 60% 70% 40% / 50% 60% 30% 60%; }
        }

        .blob {
            animation: blob 8s ease-in-out infinite;
            background: linear-gradient(45deg, #3b82f6, #f59e0b);
            opacity: 0.3;
            filter: blur(40px);
        }

        /* Glitch Effect */
        .glitch {
            position: relative;
        }

        .glitch::before,
        .glitch::after {
            content: attr(data-text);
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
        }

        .glitch::before {
            left: 2px;
            text-shadow: -2px 0 #ff00c1;
            clip: rect(44px, 450px, 56px, 0);
            animation: glitch-anim 5s infinite linear alternate-reverse;
        }

        .glitch::after {
            left: -2px;
            text-shadow: -2px 0 #00fff9;
            clip: rect(44px, 450px, 56px, 0);
            animation: glitch-anim2 5s infinite linear alternate-reverse;
        }

        @keyframes glitch-anim {
            0% { clip: rect(31px, 9999px, 94px, 0); }
            20% { clip: rect(58px, 9999px, 12px, 0); }
            40% { clip: rect(12px, 9999px, 76px, 0); }
            60% { clip: rect(85px, 9999px, 34px, 0); }
            80% { clip: rect(43px, 9999px, 91px, 0); }
            100% { clip: rect(67px, 9999px, 23px, 0); }
        }

        @keyframes glitch-anim2 {
            0% { clip: rect(65px, 9999px, 99px, 0); }
            20% { clip: rect(12px, 9999px, 45px, 0); }
            40% { clip: rect(78px, 9999px, 23px, 0); }
            60% { clip: rect(34px, 9999px, 67px, 0); }
            80% { clip: rect(91px, 9999px, 12px, 0); }
            100% { clip: rect(23px, 9999px, 85px, 0); }
        }

        /* Neon Glow */
        .neon-glow {
            box-shadow: 0 0 20px rgba(59, 130, 246, 0.5),
                        0 0 40px rgba(59, 130, 246, 0.3),
                        0 0 60px rgba(59, 130, 246, 0.1);
        }

        /* Scrollbar */
        ::-webkit-scrollbar {
            width: 10px;
        }

        ::-webkit-scrollbar-track {
            background: #0f172a;
        }

        ::-webkit-scrollbar-thumb {
            background: linear-gradient(180deg, #3b82f6, #f59e0b);
            border-radius: 5px;
        }

        /* Subject Cards Stacked */
        .subject-stack {
            perspective: 1000px;
        }

        .subject-card {
            transition: all 0.6s cubic-bezier(0.23, 1, 0.32, 1);
        }

        /* Liquid Fill Button */
        .liquid-btn {
            position: relative;
            overflow: hidden;
            z-index: 1;
        }

        .liquid-btn::before {
            content: '';
            position: absolute;
            top: 50%;
            left: 50%;
            width: 0;
            height: 0;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.2);
            transform: translate(-50%, -50%);
            transition: width 0.6s, height 0.6s;
            z-index: -1;
        }

        .liquid-btn:hover::before {
            width: 300px;
            height: 300px;
        }

        /* Typewriter Effect */
        .typewriter {
            overflow: hidden;
            border-right: 3px solid #f59e0b;
            white-space: nowrap;
            animation: typing 3.5s steps(40, end), blink-caret 0.75s step-end infinite;
        }

        @keyframes typing {
            from { width: 0 }
            to { width: 100% }
        }

        @keyframes blink-caret {
            from, to { border-color: transparent }
            50% { border-color: #f59e0b }
        }

        /* 3D Tilt Card */
        .tilt-card {
            transform-style: preserve-3d;
            transition: transform 0.1s;
        }

        .tilt-content {
            transform: translateZ(50px);
        }

        /* Reveal Animation Classes */
        .reveal-up {
            opacity: 0;
            transform: translateY(50px);
        }

        .reveal-left {
            opacity: 0;
            transform: translateX(-50px);
        }

        .reveal-scale {
            opacity: 0;
            transform: scale(0.8);
        }

        /* Grid Pattern */
        .grid-pattern {
            background-image: 
                linear-gradient(rgba(59, 130, 246, 0.1) 1px, transparent 1px),
                linear-gradient(90deg, rgba(59, 130, 246, 0.1) 1px, transparent 1px);
            background-size: 50px 50px;
        }

        /* Loading Screen */
        .loader {
            position: fixed;
            inset: 0;
            background: #0f172a;
            z-index: 99999;
            display: flex;
            align-items: center;
            justify-content: center;
            flex-direction: column;
        }

        .loader-text {
            font-size: 3rem;
            font-weight: 800;
            background: linear-gradient(135deg, #3b82f6, #f59e0b);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.5; }
        }

        .loader-bar {
            width: 200px;
            height: 4px;
            background: rgba(255,255,255,0.1);
            border-radius: 2px;
            margin-top: 20px;
            overflow: hidden;
        }

        .loader-progress {
            height: 100%;
            background: linear-gradient(90deg, #3b82f6, #f59e0b);
            width: 0%;
            transition: width 0.3s;
        }
    </style>
</head>
<body>

    <!-- Loading Screen -->
    <div class="loader" id="loader">
        <div class="loader-text glitch" data-text="CAF STUDY HUB">CAF STUDY HUB</div>
        <div class="loader-bar">
            <div class="loader-progress" id="loader-progress"></div>
        </div>
    </div>

    <!-- Custom Cursor -->
    <div class="cursor-dot" id="cursor-dot"></div>
    <div class="cursor-outline" id="cursor-outline"></div>

    <!-- Scroll Progress -->
    <div class="scroll-progress" id="scroll-progress"></div>

    <!-- Particle Canvas -->
    <canvas id="particles-canvas"></canvas>

    <!-- Navigation -->
    <nav class="fixed w-full z-50 glass-strong border-b border-white/10 transition-all duration-300" id="navbar">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex justify-between items-center h-20">
                <div class="flex items-center space-x-3 magnetic-btn" id="logo">
                    <div class="w-12 h-12 rounded-xl bg-gradient-to-br from-blue-500 to-amber-500 flex items-center justify-center text-white font-bold text-xl shadow-lg neon-glow">
                        DM
                    </div>
                    <div>
                        <h1 class="text-xl font-bold text-white tracking-tight">Danish Murtaza</h1>
                        <p class="text-xs text-blue-400 font-medium tracking-wider">CAF STUDY HUB</p>
                    </div>
                </div>
                
                <div class="hidden md:flex space-x-1">
                    <a href="#home" class="nav-link px-6 py-2 rounded-full text-sm font-medium text-gray-300 hover:text-white hover:bg-white/10 transition-all magnetic-btn">Home</a>
                    <a href="#subjects" class="nav-link px-6 py-2 rounded-full text-sm font-medium text-gray-300 hover:text-white hover:bg-white/10 transition-all magnetic-btn">Subjects</a>
                    <a href="#resources" class="nav-link px-6 py-2 rounded-full text-sm font-medium text-gray-300 hover:text-white hover:bg-white/10 transition-all magnetic-btn">Resources</a>
                    <a href="#drives" class="nav-link px-6 py-2 rounded-full text-sm font-medium text-gray-300 hover:text-white hover:bg-white/10 transition-all magnetic-btn">Drive Links</a>
                    <a href="#official" class="nav-link px-6 py-2 rounded-full text-sm font-medium text-gray-300 hover:text-white hover:bg-white/10 transition-all magnetic-btn">Official</a>
                </div>

                <button id="mobile-menu-btn" class="md:hidden text-white hover:text-amber-400 transition magnetic-btn">
                    <i class="fas fa-bars text-2xl"></i>
                </button>
            </div>
        </div>

        <!-- Mobile Menu -->
        <div id="mobile-menu" class="hidden md:hidden glass-strong border-t border-white/10">
            <div class="px-4 pt-2 pb-4 space-y-2">
                <a href="#home" class="block px-4 py-3 text-gray-300 hover:bg-white/10 rounded-lg transition">Home</a>
                <a href="#subjects" class="block px-4 py-3 text-gray-300 hover:bg-white/10 rounded-lg transition">Subjects</a>
                <a href="#resources" class="block px-4 py-3 text-gray-300 hover:bg-white/10 rounded-lg transition">Resources</a>
                <a href="#drives" class="block px-4 py-3 text-gray-300 hover:bg-white/10 rounded-lg transition">Drive Links</a>
            </div>
        </div>
    </nav>

    <!-- Hero Section -->
    <section id="home" class="relative min-h-screen flex items-center justify-center overflow-hidden grid-pattern">
        <!-- Background Blobs -->
        <div class="absolute top-20 left-10 w-72 h-72 blob floating"></div>
        <div class="absolute bottom-20 right-10 w-96 h-96 blob floating-reverse" style="animation-delay: -2s;"></div>
        <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-[600px] h-[600px] blob floating-slow opacity-20"></div>

        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 relative z-10">
            <div class="grid lg:grid-cols-2 gap-12 items-center">
                <div class="space-y-8 parallax-layer" data-speed="0.5">
                    <div class="inline-flex items-center px-4 py-2 rounded-full glass text-blue-400 text-sm font-semibold border border-blue-500/30 reveal-up">
                        <i class="fas fa-graduation-cap mr-2"></i>
                        <span class="typewriter">ICAP Certified Resources</span>
                    </div>
                    
                    <h1 class="text-5xl lg:text-7xl font-bold leading-tight reveal-up">
                        Master Your <br>
                        <span class="gradient-text glitch" data-text="CAF Journey">CAF Journey</span>
                    </h1>
                    
                    <p class="text-xl text-gray-400 leading-relaxed max-w-lg reveal-up">
                        A comprehensive study hub for ICAP CAF students. Access organized study materials, chapter-wise resources, official ICAP content, and video lectures in an immersive 3D environment.
                    </p>
                    
                    <div class="flex flex-wrap gap-4 reveal-up">
                        <a href="#subjects" class="magnetic-btn liquid-btn px-8 py-4 bg-gradient-to-r from-blue-600 to-blue-500 text-white rounded-full font-semibold hover:shadow-lg hover:shadow-blue-500/50 transition-all transform hover:-translate-y-1">
                            Explore Subjects
                            <i class="fas fa-arrow-right ml-2"></i>
                        </a>
                        <a href="#drives" class="magnetic-btn px-8 py-4 glass text-white border border-white/20 rounded-full font-semibold hover:bg-white/10 transition-all">
                            Access Drives
                        </a>
                    </div>

                    <div class="flex items-center space-x-8 text-sm text-gray-500 reveal-up">
                        <div class="flex items-center space-x-2">
                            <div class="w-2 h-2 rounded-full bg-green-500 animate-pulse"></div>
                            <span>8 CAF Subjects</span>
                        </div>
                        <div class="flex items-center space-x-2">
                            <div class="w-2 h-2 rounded-full bg-amber-500 animate-pulse" style="animation-delay: 0.5s;"></div>
                            <span>200+ Lectures</span>
                        </div>
                        <div class="flex items-center space-x-2">
                            <div class="w-2 h-2 rounded-full bg-blue-500 animate-pulse" style="animation-delay: 1s;"></div>
                            <span>100% Free</span>
                        </div>
                    </div>
                </div>

                <div class="relative parallax-layer" data-speed="-0.3">
                    <div class="absolute inset-0 bg-gradient-to-r from-blue-500 to-amber-500 rounded-3xl blur-3xl opacity-20 floating"></div>
                    
                    <!-- 3D Card Stack -->
                    <div class="relative subject-stack h-[500px]">
                        <div class="subject-card absolute inset-0 glass rounded-3xl p-8 border border-white/10 transform rotate-3 hover:rotate-0 transition-all cursor-pointer" style="z-index: 4;">
                            <div class="h-full flex flex-col justify-between">
                                <div class="flex justify-between items-start">
                                    <div class="w-14 h-14 rounded-2xl bg-gradient-to-br from-blue-500 to-blue-600 flex items-center justify-center text-2xl shadow-lg">
                                        <i class="fas fa-calculator text-white"></i>
                                    </div>
                                    <span class="px-3 py-1 rounded-full bg-blue-500/20 text-blue-400 text-xs font-bold">CAF-1</span>
                                </div>
                                <div>
                                    <h3 class="text-2xl font-bold text-white mb-2">Financial Accounting</h3>
                                    <p class="text-gray-400 text-sm">Reporting Standards & Framework</p>
                                    <div class="mt-4 h-1 bg-gray-700 rounded-full overflow-hidden">
                                        <div class="h-full bg-blue-500 w-3/4 rounded-full"></div>
                                    </div>
                                </div>
                            </div>
                        </div>

                        <div class="subject-card absolute inset-0 glass rounded-3xl p-8 border border-white/10 transform -rotate-2 translate-y-4 translate-x-4 hover:rotate-0 hover:translate-y-0 hover:translate-x-0 transition-all cursor-pointer" style="z-index: 3;">
                            <div class="h-full flex flex-col justify-between">
                                <div class="flex justify-between items-start">
                                    <div class="w-14 h-14 rounded-2xl bg-gradient-to-br from-green-500 to-green-600 flex items-center justify-center text-2xl shadow-lg">
                                        <i class="fas fa-file-invoice-dollar text-white"></i>
                                    </div>
                                    <span class="px-3 py-1 rounded-full bg-green-500/20 text-green-400 text-xs font-bold">CAF-2</span>
                                </div>
                                <div>
                                    <h3 class="text-2xl font-bold text-white mb-2">Taxation</h3>
                                    <p class="text-gray-400 text-sm">Principles & Compliance</p>
                                </div>
                            </div>
                        </div>

                        <div class="subject-card absolute inset-0 glass rounded-3xl p-8 border border-white/10 transform rotate-1 translate-y-8 translate-x-8 hover:rotate-0 hover:translate-y-0 hover:translate-x-0 transition-all cursor-pointer" style="z-index: 2;">
                            <div class="h-full flex flex-col justify-between">
                                <div class="flex justify-between items-start">
                                    <div class="w-14 h-14 rounded-2xl bg-gradient-to-br from-purple-500 to-purple-600 flex items-center justify-center text-2xl shadow-lg">
                                        <i class="fas fa-database text-white"></i>
                                    </div>
                                    <span class="px-3 py-1 rounded-full bg-purple-500/20 text-purple-400 text-xs font-bold">CAF-3</span>
                                </div>
                                <div>
                                    <h3 class="text-2xl font-bold text-white mb-2">Data & Systems</h3>
                                    <p class="text-gray-400 text-sm">Risk Management</p>
                                </div>
                            </div>
                        </div>

                        <div class="subject-card absolute inset-0 glass rounded-3xl p-8 border border-white/10 transform -rotate-3 translate-y-12 translate-x-12 hover:rotate-0 hover:translate-y-0 hover:translate-x-0 transition-all cursor-pointer" style="z-index: 1;">
                            <div class="h-full flex flex-col justify-between">
                                <div class="flex justify-between items-start">
                                    <div class="w-14 h-14 rounded-2xl bg-gradient-to-br from-amber-500 to-amber-600 flex items-center justify-center text-2xl shadow-lg">
                                        <i class="fas fa-balance-scale text-white"></i>
                                    </div>
                                    <span class="px-3 py-1 rounded-full bg-amber-500/20 text-amber-400 text-xs font-bold">CAF-4</span>
                                </div>
                                <div>
                                    <h3 class="text-2xl font-bold text-white mb-2">Business Law</h3>
                                    <p class="text-gray-400 text-sm">Legal Framework</p>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- Scroll Indicator -->
        <div class="absolute bottom-8 left-1/2 -translate-x-1/2 flex flex-col items-center space-y-2 opacity-50">
            <span class="text-xs tracking-widest uppercase">Scroll</span>
            <div class="w-6 h-10 border-2 border-white/30 rounded-full flex justify-center p-2">
                <div class="w-1 h-2 bg-white rounded-full animate-bounce"></div>
            </div>
        </div>
    </section>

    <!-- Quick Stats with 3D Counter -->
    <section class="py-20 relative overflow-hidden">
        <div class="absolute inset-0 bg-gradient-to-r from-blue-900/20 to-amber-900/20"></div>
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 relative z-10">
            <div class="grid grid-cols-2 md:grid-cols-4 gap-8 text-center">
                <div class="glass rounded-2xl p-8 transform hover:scale-105 transition-all reveal-up">
                    <div class="text-5xl font-bold mb-2 gradient-text counter" data-target="8">0</div>
                    <div class="text-gray-400 text-sm tracking-wider uppercase">CAF Subjects</div>
                </div>
                <div class="glass rounded-2xl p-8 transform hover:scale-105 transition-all reveal-up" style="transition-delay: 0.1s;">
                    <div class="text-5xl font-bold mb-2 gradient-text counter" data-target="50">0</div>
                    <div class="text-gray-400 text-sm tracking-wider uppercase">Drive Folders</div>
                </div>
                <div class="glass rounded-2xl p-8 transform hover:scale-105 transition-all reveal-up" style="transition-delay: 0.2s;">
                    <div class="text-5xl font-bold mb-2 gradient-text counter" data-target="200">0</div>
                    <div class="text-gray-400 text-sm tracking-wider uppercase">Video Lectures</div>
                </div>
                <div class="glass rounded-2xl p-8 transform hover:scale-105 transition-all reveal-up" style="transition-delay: 0.3s;">
                    <div class="text-5xl font-bold mb-2 gradient-text">100%</div>
                    <div class="text-gray-400 text-sm tracking-wider uppercase">Free Access</div>
                </div>
            </div>
        </div>
    </section>

    <!-- Drive Links Section with 3D Tilt Cards -->
    <section id="drives" class="py-32 relative">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="text-center mb-20">
                <h2 class="text-5xl font-bold mb-6 reveal-up">
                    Quick Access <span class="gradient-text">Drive Links</span>
                </h2>
                <p class="text-xl text-gray-400 max-w-2xl mx-auto reveal-up">
                    Direct links to all study materials organized by subject groups. Hover to explore in 3D space.
                </p>
            </div>

            <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
                <!-- Drive Card 1 -->
                <div class="tilt-card gradient-border p-1 reveal-up" onclick="window.open('https://drive.google.com/drive/folders/15vdglNH0iBiKNCRstPVeG2JlhyJ1LDug', '_blank')">
                    <div class="bg-slate-900 rounded-[14px] p-8 h-full flex flex-col justify-between relative overflow-hidden group cursor-pointer">
                        <div class="absolute inset-0 bg-gradient-to-br from-blue-600/20 to-transparent opacity-0 group-hover:opacity-100 transition-opacity"></div>
                        
                        <div class="relative z-10">
                            <div class="flex items-start justify-between mb-6">
                                <div class="w-14 h-14 rounded-2xl bg-gradient-to-br from-blue-500 to-blue-600 flex items-center justify-center text-2xl shadow-lg group-hover:scale-110 transition-transform">
                                    <i class="fas fa-folder-open text-white"></i>
                                </div>
                                <span class="px-3 py-1 bg-blue-500/20 text-blue-400 text-xs font-bold rounded-full border border-blue-500/30">Group A</span>
                            </div>
                            
                            <h3 class="text-xl font-bold text-white mb-3 group-hover:text-blue-400 transition-colors">CAF Notes & Chapters</h3>
                            <p class="text-gray-400 text-sm mb-6">Chapter-wise notes for Business Law, Company Introduction, Directors, and Memorandum Articles.</p>
                            
                            <div class="flex items-center text-blue-400 font-semibold text-sm group-hover:translate-x-2 transition-transform">
                                <span>Access Drive</span>
                                <i class="fas fa-external-link-alt ml-2"></i>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Drive Card 2 -->
                <div class="tilt-card gradient-border p-1 reveal-up" style="transition-delay: 0.1s;" onclick="window.open('https://drive.google.com/drive/folders/1EaTnMuDIW3h8Iw8t0WME-VkDene_5oND', '_blank')">
                    <div class="bg-slate-900 rounded-[14px] p-8 h-full flex flex-col justify-between relative overflow-hidden group cursor-pointer">
                        <div class="absolute inset-0 bg-gradient-to-br from-green-600/20 to-transparent opacity-0 group-hover:opacity-100 transition-opacity"></div>
                        
                        <div class="relative z-10">
                            <div class="flex items-start justify-between mb-6">
                                <div class="w-14 h-14 rounded-2xl bg-gradient-to-br from-green-500 to-green-600 flex items-center justify-center text-2xl shadow-lg group-hover:scale-110 transition-transform">
                                    <i class="fas fa-book text-white"></i>
                                </div>
                                <span class="px-3 py-1 bg-green-500/20 text-green-400 text-xs font-bold rounded-full border border-green-500/30">All Levels</span>
                            </div>
                            
                            <h3 class="text-xl font-bold text-white mb-3 group-hover:text-green-400 transition-colors">CA Study Material Hub</h3>
                            <p class="text-gray-400 text-sm mb-6">Comprehensive repository including PRC, CAF, ACCA materials, firms data, and guidance documents.</p>
                            
                            <div class="flex items-center text-green-400 font-semibold text-sm group-hover:translate-x-2 transition-transform">
                                <span>Access Drive</span>
                                <i class="fas fa-external-link-alt ml-2"></i>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Drive Card 3 -->
                <div class="tilt-card gradient-border p-1 reveal-up" style="transition-delay: 0.2s;" onclick="window.open('https://drive.google.com/drive/folders/1yYmQfjOf5hWfY2g6C0axnV9gNM_8kXzE', '_blank')">
                    <div class="bg-slate-900 rounded-[14px] p-8 h-full flex flex-col justify-between relative overflow-hidden group cursor-pointer">
                        <div class="absolute inset-0 bg-gradient-to-br from-purple-600/20 to-transparent opacity-0 group-hover:opacity-100 transition-opacity"></div>
                        
                        <div class="relative z-10">
                            <div class="flex items-start justify-between mb-6">
                                <div class="w-14 h-14 rounded-2xl bg-gradient-to-br from-purple-500 to-purple-600 flex items-center justify-center text-2xl shadow-lg group-hover:scale-110 transition-transform">
                                    <i class="fas fa-graduation-cap text-white"></i>
                                </div>
                                <span class="px-3 py-1 bg-purple-500/20 text-purple-400 text-xs font-bold rounded-full border border-purple-500/30">Complete</span>
                            </div>
                            
                            <h3 class="text-xl font-bold text-white mb-3 group-hover:text-purple-400 transition-colors">CAF All Books & Handouts</h3>
                            <p class="text-gray-400 text-sm mb-6">Official ICAP books, attempt-wise past papers with solutions, marking plans, and examiner comments.</p>
                            
                            <div class="flex items-center text-purple-400 font-semibold text-sm group-hover:translate-x-2 transition-transform">
                                <span>Access Drive</span>
                                <i class="fas fa-external-link-alt ml-2"></i>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Drive Card 4 -->
                <div class="tilt-card gradient-border p-1 reveal-up" onclick="window.open('https://drive.google.com/drive/folders/1-LsXYawDiR7hL_iWTSyP6mItFcUsgsLe', '_blank')">
                    <div class="bg-slate-900 rounded-[14px] p-8 h-full flex flex-col justify-between relative overflow-hidden group cursor-pointer">
                        <div class="absolute inset-0 bg-gradient-to-br from-amber-600/20 to-transparent opacity-0 group-hover:opacity-100 transition-opacity"></div>
                        
                        <div class="relative z-10">
                            <div class="flex items-start justify-between mb-6">
                                <div class="w-14 h-14 rounded-2xl bg-gradient-to-br from-amber-500 to-amber-600 flex items-center justify-center text-2xl shadow-lg group-hover:scale-110 transition-transform">
                                    <i class="fas fa-file-alt text-white"></i>
                                </div>
                                <span class="px-3 py-1 bg-amber-500/20 text-amber-400 text-xs font-bold rounded-full border border-amber-500/30">CA Aspirants</span>
                            </div>
                            
                            <h3 class="text-xl font-bold text-white mb-3 group-hover:text-amber-400 transition-colors">CAF Books & Resources</h3>
                            <p class="text-gray-400 text-sm mb-6">Group A & B books, IFRS 2025, Gripping GAAP, exam statistics, and mock exams.</p>
                            
                            <div class="flex items-center text-amber-400 font-semibold text-sm group-hover:translate-x-2 transition-transform">
                                <span>Access Drive</span>
                                <i class="fas fa-external-link-alt ml-2"></i>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Drive Card 5 -->
                <div class="tilt-card gradient-border p-1 reveal-up" style="transition-delay: 0.1s;" onclick="window.open('https://mega.nz/folder/P9om2JpY#e8DFeG4O1TG0NvGQyfkEDw/folder/b5QTHaYZ', '_blank')">
                    <div class="bg-slate-900 rounded-[14px] p-8 h-full flex flex-col justify-between relative overflow-hidden group cursor-pointer">
                        <div class="absolute inset-0 bg-gradient-to-br from-red-600/20 to-transparent opacity-0 group-hover:opacity-100 transition-opacity"></div>
                        
                        <div class="relative z-10">
                            <div class="flex items-start justify-between mb-6">
                                <div class="w-14 h-14 rounded-2xl bg-gradient-to-br from-red-500 to-red-600 flex items-center justify-center text-2xl shadow-lg group-hover:scale-110 transition-transform">
                                    <i class="fas fa-cloud text-white"></i>
                                </div>
                                <span class="px-3 py-1 bg-red-500/20 text-red-400 text-xs font-bold rounded-full border border-red-500/30">Mega.nz</span>
                            </div>
                            
                            <h3 class="text-xl font-bold text-white mb-3 group-hover:text-red-400 transition-colors">Additional Resources</h3>
                            <p class="text-gray-400 text-sm mb-6">Supplementary study materials and reference documents hosted on Mega cloud storage.</p>
                            
                            <div class="flex items-center text-red-400 font-semibold text-sm group-hover:translate-x-2 transition-transform">
                                <span>Access Drive</span>
                                <i class="fas fa-external-link-alt ml-2"></i>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Official ICAP -->
                <div class="tilt-card gradient-border p-1 reveal-up" style="transition-delay: 0.2s;" onclick="window.open('https://icap.org.pk/students/study-resources/education-scheme-2025/study-resources/', '_blank')">
                    <div class="bg-slate-900 rounded-[14px] p-8 h-full flex flex-col justify-between relative overflow-hidden group cursor-pointer">
                        <div class="absolute inset-0 bg-gradient-to-br from-gray-600/20 to-transparent opacity-0 group-hover:opacity-100 transition-opacity"></div>
                        
                        <div class="relative z-10">
                            <div class="flex items-start justify-between mb-6">
                                <div class="w-14 h-14 rounded-2xl bg-gradient-to-br from-gray-700 to-gray-800 flex items-center justify-center text-2xl shadow-lg group-hover:scale-110 transition-transform border border-gray-600">
                                    <i class="fas fa-university text-white"></i>
                                </div>
                                <span class="px-3 py-1 bg-gray-500/20 text-gray-400 text-xs font-bold rounded-full border border-gray-500/30">Official</span>
                            </div>
                            
                            <h3 class="text-xl font-bold text-white mb-3 group-hover:text-gray-300 transition-colors">ICAP Official Resources</h3>
                            <p class="text-gray-400 text-sm mb-6">Direct access to ICAP's official study texts, question banks, model exam papers, and syllabi.</p>
                            
                            <div class="flex items-center text-gray-400 font-semibold text-sm group-hover:translate-x-2 transition-transform">
                                <span>Visit Website</span>
                                <i class="fas fa-external-link-alt ml-2"></i>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Subjects Section with Interactive 3D -->
    <section id="subjects" class="py-32 relative">
        <div class="absolute inset-0 bg-gradient-to-b from-transparent via-blue-900/10 to-transparent"></div>
        
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 relative z-10">
            <div class="text-center mb-16">
                <h2 class="text-5xl font-bold mb-6 reveal-up">
                    CAF <span class="gradient-text">Subjects</span>
                </h2>
                <p class="text-xl text-gray-400 reveal-up">Select a subject to explore chapter-wise resources in an immersive interface</p>
            </div>

            <!-- Subject Selector -->
            <div class="flex flex-wrap justify-center gap-3 mb-12 reveal-up" id="subject-tabs">
                <button onclick="switchSubject('caf1')" class="subject-tab tab-active magnetic-btn px-6 py-3 rounded-full font-semibold transition-all border border-transparent" data-subject="caf1">
                    CAF-1 FAR
                </button>
                <button onclick="switchSubject('caf2')" class="subject-tab magnetic-btn px-6 py-3 rounded-full font-semibold transition-all border border-white/10 bg-white/5 text-gray-400 hover:bg-white/10" data-subject="caf2">
                    CAF-2 TPC
                </button>
                <button onclick="switchSubject('caf3')" class="subject-tab magnetic-btn px-6 py-3 rounded-full font-semibold transition-all border border-white/10 bg-white/5 text-gray-400 hover:bg-white/10" data-subject="caf3">
                    CAF-3 DSR
                </button>
                <button onclick="switchSubject('caf4')" class="subject-tab magnetic-btn px-6 py-3 rounded-full font-semibold transition-all border border-white/10 bg-white/5 text-gray-400 hover:bg-white/10" data-subject="caf4">
                    CAF-4 BLD
                </button>
                <button onclick="switchSubject('caf5')" class="subject-tab magnetic-btn px-6 py-3 rounded-full font-semibold transition-all border border-white/10 bg-white/5 text-gray-400 hover:bg-white/10" data-subject="caf5">
                    CAF-5 MA
                </button>
                <button onclick="switchSubject('caf6')" class="subject-tab magnetic-btn px-6 py-3 rounded-full font-semibold transition-all border border-white/10 bg-white/5 text-gray-400 hover:bg-white/10" data-subject="caf6">
                    CAF-6 CR
                </button>
                <button onclick="switchSubject('caf7')" class="subject-tab magnetic-btn px-6 py-3 rounded-full font-semibold transition-all border border-white/10 bg-white/5 text-gray-400 hover:bg-white/10" data-subject="caf7">
                    CAF-7 BIA
                </button>
                <button onclick="switchSubject('caf8')" class="subject-tab magnetic-btn px-6 py-3 rounded-full font-semibold transition-all border border-white/10 bg-white/5 text-gray-400 hover:bg-white/10" data-subject="caf8">
                    CAF-8 AAE
                </button>
            </div>

            <!-- Subject Content -->
            <div id="subject-content" class="glass rounded-3xl p-8 border border-white/10 min-h-[600px] relative overflow-hidden">
                <!-- Content loaded dynamically -->
            </div>
        </div>
    </section>

    <!-- Official Resources with Parallax -->
    <section id="official" class="py-32 relative overflow-hidden">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="grid lg:grid-cols-2 gap-16 items-center">
                <div class="space-y-8 reveal-left">
                    <h2 class="text-5xl font-bold">
                        Official <span class="gradient-text">ICAP Resources</span>
                    </h2>
                    <p class="text-xl text-gray-400 leading-relaxed">
                        Access the official Institute of Chartered Accountants of Pakistan digital study material platform featuring interactive features, audio read-aloud, and progress tracking.
                    </p>

                    <div class="space-y-4">
                        <div class="glass rounded-2xl p-6 border border-white/10 hover:border-blue-500/50 transition-all group cursor-pointer" onclick="window.open('https://icap.org.pk/students/study-resources/icap-digital-study-material/', '_blank')">
                            <div class="flex items-start space-x-4">
                                <div class="w-12 h-12 rounded-xl bg-blue-500/20 text-blue-400 flex items-center justify-center flex-shrink-0 group-hover:scale-110 transition-transform">
                                    <i class="fas fa-book-reader text-xl"></i>
                                </div>
                                <div>
                                    <h4 class="font-bold text-white text-lg mb-1 group-hover:text-blue-400 transition-colors">Digital Study Material</h4>
                                    <p class="text-gray-400 text-sm mb-2">Interactive platform with searchable text, highlights, and notes features.</p>
                                    <span class="text-blue-400 text-sm font-semibold flex items-center">
                                        Access Platform <i class="fas fa-arrow-right ml-2 group-hover:translate-x-1 transition-transform"></i>
                                    </span>
                                </div>
                            </div>
                        </div>

                        <div class="glass rounded-2xl p-6 border border-white/10 hover:border-green-500/50 transition-all group cursor-pointer" onclick="window.open('https://icap.org.pk/students/study-resources/education-scheme-2025/study-resources/', '_blank')">
                            <div class="flex items-start space-x-4">
                                <div class="w-12 h-12 rounded-xl bg-green-500/20 text-green-400 flex items-center justify-center flex-shrink-0 group-hover:scale-110 transition-transform">
                                    <i class="fas fa-file-download text-xl"></i>
                                </div>
                                <div>
                                    <h4 class="font-bold text-white text-lg mb-1 group-hover:text-green-400 transition-colors">Study Texts & Question Banks</h4>
                                    <p class="text-gray-400 text-sm mb-2">Download official study texts, question banks, and model exam papers.</p>
                                    <span class="text-green-400 text-sm font-semibold flex items-center">
                                        Download Resources <i class="fas fa-arrow-right ml-2 group-hover:translate-x-1 transition-transform"></i>
                                    </span>
                                </div>
                            </div>
                        </div>

                        <div class="glass rounded-2xl p-6 border border-white/10 hover:border-amber-500/50 transition-all group cursor-pointer" onclick="window.open('https://icap.org.pk/examiner-comments/caf/', '_blank')">
                            <div class="flex items-start space-x-4">
                                <div class="w-12 h-12 rounded-xl bg-amber-500/20 text-amber-400 flex items-center justify-center flex-shrink-0 group-hover:scale-110 transition-transform">
                                    <i class="fas fa-clipboard-check text-xl"></i>
                                </div>
                                <div>
                                    <h4 class="font-bold text-white text-lg mb-1 group-hover:text-amber-400 transition-colors">Examination Guidance</h4>
                                    <p class="text-gray-400 text-sm mb-2">Specific guidance for CAF exams, marking plans, and examiner comments.</p>
                                    <span class="text-amber-400 text-sm font-semibold flex items-center">
                                        View Guidance <i class="fas fa-arrow-right ml-2 group-hover:translate-x-1 transition-transform"></i>
                                    </span>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="relative reveal-scale">
                    <div class="absolute inset-0 bg-gradient-to-r from-blue-500 to-amber-500 rounded-3xl blur-3xl opacity-20"></div>
                    <div class="relative glass rounded-3xl p-8 border border-white/10">
                        <div class="flex items-center justify-between mb-8">
                            <h3 class="text-2xl font-bold text-white">ICAP Student Portal</h3>
                            <div class="flex space-x-2">
                                <div class="w-3 h-3 rounded-full bg-red-500"></div>
                                <div class="w-3 h-3 rounded-full bg-yellow-500"></div>
                                <div class="w-3 h-3 rounded-full bg-green-500"></div>
                            </div>
                        </div>

                        <div class="space-y-4">
                            <div class="p-4 rounded-xl bg-white/5 border border-white/10">
                                <div class="flex justify-between items-center mb-2">
                                    <span class="text-sm text-gray-400">Digital Platform Access</span>
                                    <span class="text-xs bg-green-500/20 text-green-400 px-2 py-1 rounded">Active</span>
                                </div>
                                <div class="h-2 bg-gray-700 rounded-full overflow-hidden">
                                    <div class="h-full bg-gradient-to-r from-blue-500 to-green-500 w-full rounded-full"></div>
                                </div>
                            </div>

                            <div class="grid grid-cols-2 gap-4">
                                <div class="p-4 rounded-xl bg-white/5 border border-white/10 text-center group hover:bg-white/10 transition-colors cursor-pointer">
                                    <i class="fas fa-highlighter text-2xl text-blue-400 mb-2 group-hover:scale-110 transition-transform block"></i>
                                    <span class="text-xs text-gray-400">Highlights</span>
                                </div>
                                <div class="p-4 rounded-xl bg-white/5 border border-white/10 text-center group hover:bg-white/10 transition-colors cursor-pointer">
                                    <i class="fas fa-sticky-note text-2xl text-amber-400 mb-2 group-hover:scale-110 transition-transform block"></i>
                                    <span class="text-xs text-gray-400">Notes</span>
                                </div>
                                <div class="p-4 rounded-xl bg-white/5 border border-white/10 text-center group hover:bg-white/10 transition-colors cursor-pointer">
                                    <i class="fas fa-volume-up text-2xl text-green-400 mb-2 group-hover:scale-110 transition-transform block"></i>
                                    <span class="text-xs text-gray-400">Audio</span>
                                </div>
                                <div class="p-4 rounded-xl bg-white/5 border border-white/10 text-center group hover:bg-white/10 transition-colors cursor-pointer">
                                    <i class="fas fa-chart-line text-2xl text-purple-400 mb-2 group-hover:scale-110 transition-transform block"></i>
                                    <span class="text-xs text-gray-400">Progress</span>
                                </div>
                            </div>

                            <button onclick="window.open('https://student.icap.org.pk/', '_blank')" class="w-full py-4 bg-gradient-to-r from-blue-600 to-blue-500 text-white rounded-xl font-semibold hover:shadow-lg hover:shadow-blue-500/50 transition-all transform hover:-translate-y-1">
                                Login to Student Portal
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Video Resources with Hover Effects -->
    <section class="py-32 relative bg-slate-900/50">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="text-center mb-16">
                <h2 class="text-5xl font-bold mb-6 reveal-up">
                    Video <span class="gradient-text">Lecture Resources</span>
                </h2>
                <p class="text-xl text-gray-400 reveal-up">Curated YouTube channels and lecture series for CAF preparation</p>
            </div>

            <div class="grid md:grid-cols-2 lg:grid-cols-4 gap-6">
                <a href="https://www.youtube.com/results?search_query=icap+caf+1+financial+accounting+reporting" target="_blank" class="group block glass rounded-2xl p-6 border border-white/10 hover:border-red-500/50 transition-all hover:-translate-y-2 reveal-up">
                    <div class="w-16 h-16 rounded-2xl bg-red-500/20 flex items-center justify-center mb-4 group-hover:scale-110 transition-transform">
                        <i class="fab fa-youtube text-3xl text-red-500"></i>
                    </div>
                    <h3 class="font-bold text-xl text-white mb-2 group-hover:text-red-400 transition-colors">CAF-1 FAR</h3>
                    <p class="text-gray-400 text-sm">Financial Accounting & Reporting lectures and tutorials</p>
                    <div class="mt-4 flex items-center text-red-400 text-sm font-semibold opacity-0 group-hover:opacity-100 transition-opacity">
                        Watch Now <i class="fas fa-arrow-right ml-2"></i>
                    </div>
                </a>

                <a href="https://www.youtube.com/results?search_query=icap+caf+2+taxation+principles" target="_blank" class="group block glass rounded-2xl p-6 border border-white/10 hover:border-red-500/50 transition-all hover:-translate-y-2 reveal-up" style="transition-delay: 0.1s;">
                    <div class="w-16 h-16 rounded-2xl bg-red-500/20 flex items-center justify-center mb-4 group-hover:scale-110 transition-transform">
                        <i class="fab fa-youtube text-3xl text-red-500"></i>
                    </div>
                    <h3 class="font-bold text-xl text-white mb-2 group-hover:text-red-400 transition-colors">CAF-2 TPC</h3>
                    <p class="text-gray-400 text-sm">Taxation Principles & Compliance video series</p>
                    <div class="mt-4 flex items-center text-red-400 text-sm font-semibold opacity-0 group-hover:opacity-100 transition-opacity">
                        Watch Now <i class="fas fa-arrow-right ml-2"></i>
                    </div>
                </a>

                <a href="https://www.youtube.com/results?search_query=icap+caf+3+data+systems+risks" target="_blank" class="group block glass rounded-2xl p-6 border border-white/10 hover:border-red-500/50 transition-all hover:-translate-y-2 reveal-up" style="transition-delay: 0.2s;">
                    <div class="w-16 h-16 rounded-2xl bg-red-500/20 flex items-center justify-center mb-4 group-hover:scale-110 transition-transform">
                        <i class="fab fa-youtube text-3xl text-red-500"></i>
                    </div>
                    <h3 class="font-bold text-xl text-white mb-2 group-hover:text-red-400 transition-colors">CAF-3 DSR</h3>
                    <p class="text-gray-400 text-sm">Data, Systems & Risks comprehensive lectures</p>
                    <div class="mt-4 flex items-center text-red-400 text-sm font-semibold opacity-0 group-hover:opacity-100 transition-opacity">
                        Watch Now <i class="fas fa-arrow-right ml-2"></i>
                    </div>
                </a>

                <a href="https://www.youtube.com/results?search_query=icap+caf+4+business+law" target="_blank" class="group block glass rounded-2xl p-6 border border-white/10 hover:border-red-500/50 transition-all hover:-translate-y-2 reveal-up" style="transition-delay: 0.3s;">
                    <div class="w-16 h-16 rounded-2xl bg-red-500/20 flex items-center justify-center mb-4 group-hover:scale-110 transition-transform">
                        <i class="fab fa-youtube text-3xl text-red-500"></i>
                    </div>
                    <h3 class="font-bold text-xl text-white mb-2 group-hover:text-red-400 transition-colors">CAF-4 BLD</h3>
                    <p class="text-gray-400 text-sm">Business Law Dynamics explained</p>
                    <div class="mt-4 flex items-center text-red-400 text-sm font-semibold opacity-0 group-hover:opacity-100 transition-opacity">
                        Watch Now <i class="fas fa-arrow-right ml-2"></i>
                    </div>
                </a>
            </div>

            <div class="mt-12 glass rounded-2xl p-8 border border-white/10 reveal-up">
                <div class="flex flex-col md:flex-row items-center justify-between gap-6">
                    <div class="flex items-center space-x-4">
                        <div class="w-16 h-16 rounded-full bg-gradient-to-br from-red-500 to-red-600 flex items-center justify-center text-white text-2xl">
                            <i class="fas fa-star"></i>
                        </div>
                        <div>
                            <h4 class="font-bold text-xl text-white">Recommended: Sir Murtaza Quaid</h4>
                            <p class="text-gray-400">Comprehensive Taxation Principles coverage with exam-focused approach</p>
                        </div>
                    </div>
                    <a href="https://iqsf.pk/caf-02-taxation-principles-and-compliance-by-sir-murtaza/" target="_blank" class="magnetic-btn px-8 py-4 bg-gradient-to-r from-red-600 to-red-500 text-white rounded-full font-semibold hover:shadow-lg hover:shadow-red-500/50 transition-all whitespace-nowrap">
                        View Lectures
                    </a>
                </div>
            </div>
        </div>
    </section>

    <!-- Footer -->
    <footer class="relative py-20 border-t border-white/10 bg-slate-950">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="grid md:grid-cols-4 gap-12 mb-12">
                <div class="space-y-4">
                    <div class="flex items-center space-x-3">
                        <div class="w-10 h-10 rounded-lg bg-gradient-to-br from-blue-500 to-amber-500 flex items-center justify-center text-white font-bold">DM</div>
                        <span class="text-white font-bold text-lg">Danish Murtaza</span>
                    </div>
                    <p class="text-gray-400 text-sm">Empowering CAF students with organized, accessible study resources for ICAP Pakistan qualification.</p>
                </div>
                
                <div>
                    <h4 class="text-white font-semibold mb-4">Quick Links</h4>
                    <ul class="space-y-2 text-sm text-gray-400">
                        <li><a href="https://icap.org.pk/" target="_blank" class="hover:text-blue-400 transition-colors">ICAP Official</a></li>
                        <li><a href="https://student.icap.org.pk/" target="_blank" class="hover:text-blue-400 transition-colors">Student Portal</a></li>
                        <li><a href="#subjects" class="hover:text-blue-400 transition-colors">Study Materials</a></li>
                        <li><a href="#drives" class="hover:text-blue-400 transition-colors">Drive Access</a></li>
                    </ul>
                </div>

                <div>
                    <h4 class="text-white font-semibold mb-4">CAF Levels</h4>
                    <ul class="space-y-2 text-sm text-gray-400">
                        <li><a href="#" onclick="switchSubject('caf1')" class="hover:text-blue-400 transition-colors">CAF-1 FAR</a></li>
                        <li><a href="#" onclick="switchSubject('caf2')" class="hover:text-blue-400 transition-colors">CAF-2 TPC</a></li>
                        <li><a href="#" onclick="switchSubject('caf3')" class="hover:text-blue-400 transition-colors">CAF-3 DSR</a></li>
                        <li><a href="#" onclick="switchSubject('caf4')" class="hover:text-blue-400 transition-colors">CAF-4 BLD</a></li>
                    </ul>
                </div>

                <div>
                    <h4 class="text-white font-semibold mb-4">Connect</h4>
                    <p class="text-gray-400 text-sm">Created for CAF Students by Danish Murtaza</p>
                    <p class="text-xs text-gray-500 mt-4">© 2026 All rights reserved.</p>
                </div>
            </div>
            
            <div class="pt-8 border-t border-white/10 text-center text-sm text-gray-500">
                <p>Disclaimer: This is a student resource hub. All materials belong to their respective owners. Official ICAP resources available at icap.org.pk</p>
            </div>
        </div>
    </footer>

    <script>
        // Subject Data
        const subjectsData = {
            caf1: {
                title: "CAF-1: Financial Accounting and Reporting",
                icon: "fa-calculator",
                color: "blue",
                description: "Preparation of Financial Statements, Conceptual Framework, and Accounting for Financial Transactions",
                chapters: [
                    { name: "Preparation of Financial Statements", topics: ["IAS 1 Presentation", "Statement of P&L", "Statement of FP", "Cash Flow Statements"] },
                    { name: "Conceptual Framework", topics: ["Fundamental Concepts", "Qualitative Characteristics", "Elements of FS", "Recognition Criteria"] },
                    { name: "Accounting Policies", topics: ["IAS 8 Changes", "Errors Correction", "Estimates Changes", "Discontinued Operations"] },
                    { name: "Property Plant & Equipment", topics: ["IAS 16 PPE", "Initial Recognition", "Subsequent Measurement", "Depreciation Methods"] },
                    { name: "Intangible Assets", topics: ["IAS 38", "Research & Development", "Goodwill", "Amortization"] },
                    { name: "Impairment of Assets", topics: ["IAS 36", "Impairment Indicators", "Cash Generating Units", "Reversal of Impairment"] },
                    { name: "Leases", topics: ["IFRS 16", "Lessee Accounting", "Lessor Accounting", "Sale & Leaseback"] },
                    { name: "Revenue Recognition", topics: ["IFRS 15", "5-Step Model", "Performance Obligations", "Variable Consideration"] }
                ],
                resources: [
                    { name: "Official Study Text", link: "https://icap.org.pk/students/study-resources/education-scheme-2025/study-resources/", type: "PDF" },
                    { name: "Model Exam Paper", link: "https://icap.org.pk/students/study-resources/education-scheme-2025/study-resources/", type: "Exam" },
                    { name: "Drive Notes", link: "https://drive.google.com/drive/folders/1-LsXYawDiR7hL_iWTSyP6mItFcUsgsLe", type: "Drive" }
                ]
            },
            caf2: {
                title: "CAF-2: Taxation Principles and Compliance",
                icon: "fa-file-invoice-dollar",
                color: "green",
                description: "Income Tax, Sales Tax, and Federal Excise Duty principles and compliance requirements",
                chapters: [
                    { name: "Income Tax Basics", topics: ["Scope of Income Tax", "Tax Year", "Person & Assessee", "Residential Status"] },
                    { name: "Heads of Income", topics: ["Salary", "Property Income", "Business Income", "Capital Gains", "Other Sources"] },
                    { name: "Deductions & Allowances", topics: ["Allowable Deductions", "Depreciation", "Amortization", "Tax Credits"] },
                    { name: "Tax Compliance", topics: ["Returns Filing", "Assessments", "Appeals", "Withholding Taxes"] },
                    { name: "Sales Tax", topics: ["Scope & Charge", "Registration", "Input Tax", "Output Tax", "Apportionment"] },
                    { name: "Federal Excise Duty", topics: ["Manufacturing", "Services", "Clearance", "Compliance"] }
                ],
                resources: [
                    { name: "Official Study Text", link: "https://icap.org.pk/students/study-resources/education-scheme-2025/study-resources/", type: "PDF" },
                    { name: "Question Bank", link: "https://icap.org.pk/students/study-resources/education-scheme-2025/study-resources/", type: "PDF" },
                    { name: "Sir Murtaza Lectures", link: "https://iqsf.pk/caf-02-taxation-principles-and-compliance-by-sir-murtaza/", type: "Video" }
                ]
            },
            caf3: {
                title: "CAF-3: Data, Systems and Risks",
                icon: "fa-database",
                color: "purple",
                description: "IT systems, Data Analytics, Cybersecurity, and Risk Management in digital environment",
                chapters: [
                    { name: "Types of Data and Sources", topics: ["Structured vs Unstructured", "Internal vs External", "Primary vs Secondary", "Big Data Characteristics"] },
                    { name: "Data Governance", topics: ["Data Quality", "Data Lifecycle", "Data Ownership", "Data Stewardship"] },
                    { name: "Data Analytics", topics: ["Descriptive Analytics", "Predictive Analytics", "Prescriptive Analytics", "Tools & Techniques"] },
                    { name: "Database Management", topics: ["RDBMS Concepts", "SQL Basics", "Normalization", "ACID Properties", "Data Warehousing"] },
                    { name: "IT Systems Architecture", topics: ["Client-Server", "Cloud Computing", "ERP Systems", "APIs & Integration"] },
                    { name: "Emerging Technologies", topics: ["AI & Machine Learning", "RPA", "Blockchain", "IoT", "Fintech"] },
                    { name: "Cybersecurity", topics: ["Threats & Vulnerabilities", "Encryption", "Firewalls", "MFA", "Security Protocols"] },
                    { name: "Risk Management", topics: ["Risk Identification", "Risk Assessment", "Risk Mitigation", "Business Continuity", "IT General Controls"] }
                ],
                resources: [
                    { name: "Official Study Text", link: "https://icap.org.pk/students/study-resources/education-scheme-2025/study-resources/", type: "PDF" },
                    { name: "Question Bank", link: "https://icap.org.pk/students/study-resources/education-scheme-2025/study-resources/", type: "PDF" },
                    { name: "Model Exam Questions", link: "https://icap.org.pk/students/study-resources/education-scheme-2025/study-resources/", type: "Exam" },
                    { name: "Supplementary Notes", link: "https://drive.google.com/drive/folders/1EaTnMuDIW3h8Iw8t0WME-VkDene_5oND", type: "Drive" }
                ]
            },
            caf4: {
                title: "CAF-4: Business Law Dynamics",
                icon: "fa-balance-scale",
                color: "amber",
                description: "Contract Act, Company Law, Partnership, and Business Legal Framework",
                chapters: [
                    { name: "Introduction to Law", topics: ["Sources of Law", "Legal Systems", "Court Structure", "Arbitration & Mediation"] },
                    { name: "Contract Act 1872", topics: ["Offer & Acceptance", "Consideration", "Capacity", "Free Consent", "Void Agreements"] },
                    { name: "Performance & Breach", topics: ["Performance of Contract", "Breach of Contract", "Remedies", "Indemnity & Guarantee"] },
                    { name: "Partnership Act 1932", topics: ["Formation", "Rights & Duties", "Property", "Dissolution"] },
                    { name: "Company Introduction", topics: ["Types of Companies", "Incorporation", "Memorandum", "Articles of Association"] },
                    { name: "Directors", topics: ["Appointment", "Powers & Duties", "Meetings", "Liabilities"] },
                    { name: "Corporate Governance", topics: ["SECP Regulations", "Code of Corporate Governance", "Shareholders Rights", "Disclosures"] }
                ],
                resources: [
                    { name: "Study Text Vol 1", link: "https://icap.org.pk/students/study-resources/education-scheme-2025/study-resources/", type: "PDF" },
                    { name: "Study Text Vol 2", link: "https://icap.org.pk/students/study-resources/education-scheme-2025/study-resources/", type: "PDF" },
                    { name: "Chapter Notes", link: "https://drive.google.com/drive/folders/15vdglNH0iBiKNCRstPVeG2JlhyJ1LDug", type: "Drive" },
                    { name: "Past Papers", link: "https://drive.google.com/drive/folders/1-LsXYawDiR7hL_iWTSyP6mItFcUsgsLe", type: "Drive" }
                ]
            },
            caf5: {
                title: "CAF-5: Management Accounting",
                icon: "fa-chart-pie",
                color: "indigo",
                description: "Cost accounting, Budgeting, Decision Making, and Performance Evaluation",
                chapters: [
                    { name: "Cost Classification", topics: ["By Nature", "By Function", "By Behavior", "By Decision Making"] },
                    { name: "Material & Labor", topics: ["Inventory Control", "EOQ", "Labor Costing", "Overhead Allocation"] },
                    { name: "Costing Methods", topics: ["Job Costing", "Process Costing", "Service Costing", "Joint & By-Products"] },
                    { name: "Marginal Costing", topics: ["CVP Analysis", "Break-even", "Contribution", "Limiting Factors"] },
                    { name: "Budgeting", topics: ["Types of Budgets", "Cash Budget", "Flexible Budgets", "Zero-based Budgeting"] },
                    { name: "Standard Costing", topics: ["Variance Analysis", "Material Variances", "Labor Variances", "Overhead Variances"] },
                    { name: "Decision Making", topics: ["Relevant Costs", "Make or Buy", "Shutdown Decisions", "Pricing Decisions"] }
                ],
                resources: [
                    { name: "Official Study Text", link: "https://icap.org.pk/students/study-resources/education-scheme-2025/study-resources/", type: "PDF" },
                    { name: "Model Exam Paper", link: "https://icap.org.pk/students/study-resources/education-scheme-2025/study-resources/", type: "Exam" },
                    { name: "Practice Kit", link: "https://drive.google.com/drive/folders/1EaTnMuDIW3h8Iw8t0WME-VkDene_5oND", type: "Drive" }
                ]
            },
            caf6: {
                title: "CAF-6: Corporate Reporting",
                icon: "fa-building",
                color: "rose",
                description: "Advanced financial reporting, Group accounts, and Complex standards",
                chapters: [
                    { name: "Consolidation Basics", topics: ["Control Concept", "Subsidiary Accounts", "Goodwill", "Non-controlling Interest"] },
                    { name: "Group Financial Statements", topics: ["Consolidated P&L", "Consolidated FP", "Intra-group Transactions", "Unrealized Profits"] },
                    { name: "Associates & JVs", topics: ["IAS 28 Investments", "Equity Method", "Joint Arrangements", "Proportionate Consolidation"] },
                    { name: "Foreign Operations", topics: ["IAS 21", "Functional Currency", "Translation", "Hyperinflationary Economies"] },
                    { name: "Financial Instruments", topics: ["IFRS 9", "Classification", "Measurement", "Impairment", "Hedge Accounting"] },
                    { name: "Employee Benefits", topics: ["IAS 19", "Pension Plans", "Defined Benefit", "Actuarial Gains/Losses"] },
                    { name: "Share Based Payments", topics: ["IFRS 2", "Equity Settled", "Cash Settled", "Vesting Conditions"] }
                ],
                resources: [
                    { name: "Official Study Text", link: "https://icap.org.pk/students/study-resources/education-scheme-2025/study-resources/", type: "PDF" },
                    { name: "Model Exam Paper", link: "https://icap.org.pk/students/study-resources/education-scheme-2025/study-resources/", type: "Exam" },
                    { name: "IFRS 2025", link: "https://drive.google.com/drive/folders/1-LsXYawDiR7hL_iWTSyP6mItFcUsgsLe", type: "Drive" }
                ]
            },
            caf7: {
                title: "CAF-7: Business Insights and Analysis",
                icon: "fa-lightbulb",
                color: "cyan",
                description: "Business analysis, Strategy, and Professional skills development",
                chapters: [
                    { name: "Business Environment", topics: ["PESTEL Analysis", "Porter's 5 Forces", "Industry Life Cycle", "Competitive Advantage"] },
                    { name: "Strategic Analysis", topics: ["SWOT Analysis", "BCG Matrix", "Ansoff Matrix", "Value Chain"] },
                    { name: "Financial Analysis", topics: ["Ratio Analysis", "Trend Analysis", "Cash Flow Analysis", "Valuation Techniques"] },
                    { name: "Risk Analysis", topics: ["Risk Types", "Risk Assessment", "Risk Mitigation", "Internal Controls"] },
                    { name: "Decision Making", topics: ["Investment Appraisal", "NPV & IRR", "Sensitivity Analysis", "Scenario Planning"] },
                    { name: "Professional Skills", topics: ["Communication", "Ethics", "Skepticism", "Judgment"] }
                ],
                resources: [
                    { name: "Official Study Text", link: "https://icap.org.pk/students/study-resources/education-scheme-2025/study-resources/", type: "PDF" },
                    { name: "Model Exam Paper", link: "https://icap.org.pk/students/study-resources/education-scheme-2025/study-resources/", type: "Exam" },
                    { name: "Case Studies", link: "https://drive.google.com/drive/folders/1EaTnMuDIW3h8Iw8t0WME-VkDene_5oND", type: "Drive" }
                ]
            },
            caf8: {
                title: "CAF-8: Audit and Assurance Essentials",
                icon: "fa-search",
                color: "emerald",
                description: "Audit fundamentals, Risk assessment, and Assurance engagements",
                chapters: [
                    { name: "Audit Framework", topics: ["Audit vs Assurance", "Regulatory Environment", "Ethics", "Quality Control"] },
                    { name: "Planning & Risk", topics: ["Audit Planning", "Risk Assessment", "Materiality", "Audit Strategy"] },
                    { name: "Internal Controls", topics: ["Control Environment", "Control Activities", "Monitoring", "IT Controls"] },
                    { name: "Audit Evidence", topics: ["Assertions", "Procedures", "Sampling", "Documentation"] },
                    { name: "Completion", topics: ["Subsequent Events", "Going Concern", "Written Representations", "Misstatements"] },
                    { name: "Audit Reporting", topics: ["Audit Opinion", "Modified Opinions", "Emphasis of Matter", "Other Matter"] },
                    { name: "Special Areas", topics: ["Group Audits", "Internal Audit", "Related Services", "Prospective Financial Info"] }
                ],
                resources: [
                    { name: "Official Study Text", link: "https://icap.org.pk/students/study-resources/education-scheme-2025/study-resources/", type: "PDF" },
                    { name: "Model Exam Paper", link: "https://icap.org.pk/students/study-resources/education-scheme-2025/study-resources/", type: "Exam" },
                    { name: "Audit Notes", link: "https://drive.google.com/drive/folders/1-LsXYawDiR7hL_iWTSyP6mItFcUsgsLe", type: "Drive" }
                ]
            }
        };

        // Initialize
        window.onload = function() {
            // Simulate loading
            let progress = 0;
            const loaderInterval = setInterval(() => {
                progress += Math.random() * 30;
                if (progress >= 100) {
                    progress = 100;
                    clearInterval(loaderInterval);
                    setTimeout(() => {
                        document.getElementById('loader').style.opacity = '0';
                        setTimeout(() => {
                            document.getElementById('loader').style.display = 'none';
                            initAnimations();
                        }, 500);
                    }, 500);
                }
                document.getElementById('loader-progress').style.width = progress + '%';
            }, 200);

            switchSubject('caf1');
            initParticles();
            initCursor();
            initTiltCards();
        };

        function initAnimations() {
            gsap.registerPlugin(ScrollTrigger);

            // Scroll Progress
            gsap.to('#scroll-progress', {
                scaleX: 1,
                ease: 'none',
                scrollTrigger: {
                    trigger: 'body',
                    start: 'top top',
                    end: 'bottom bottom',
                    scrub: 0.3
                }
            });

            // Reveal animations
            gsap.utils.toArray('.reveal-up').forEach(element => {
                gsap.to(element, {
                    opacity: 1,
                    y: 0,
                    duration: 1,
                    ease: 'power3.out',
                    scrollTrigger: {
                        trigger: element,
                        start: 'top 85%',
                        toggleActions: 'play none none reverse'
                    }
                });
            });

            gsap.utils.toArray('.reveal-left').forEach(element => {
                gsap.to(element, {
                    opacity: 1,
                    x: 0,
                    duration: 1,
                    ease: 'power3.out',
                    scrollTrigger: {
                        trigger: element,
                        start: 'top 85%',
                        toggleActions: 'play none none reverse'
                    }
                });
            });

            gsap.utils.toArray('.reveal-scale').forEach(element => {
                gsap.to(element, {
                    opacity: 1,
                    scale: 1,
                    duration: 1,
                    ease: 'power3.out',
                    scrollTrigger: {
                        trigger: element,
                        start: 'top 85%',
                        toggleActions: 'play none none reverse'
                    }
                });
            });

            // Parallax layers
            gsap.utils.toArray('.parallax-layer').forEach(layer => {
                const speed = layer.dataset.speed || 0.5;
                gsap.to(layer, {
                    y: -100 * speed,
                    ease: 'none',
                    scrollTrigger: {
                        trigger: layer,
                        start: 'top bottom',
                        end: 'bottom top',
                        scrub: true
                    }
                });
            });

            // Counter animation
            gsap.utils.toArray('.counter').forEach(counter => {
                const target = parseInt(counter.dataset.target);
                gsap.to(counter, {
                    innerHTML: target,
                    duration: 2,
                    snap: { innerHTML: 1 },
                    scrollTrigger: {
                        trigger: counter,
                        start: 'top 85%',
                        toggleActions: 'play none none reverse'
                    }
                });
            });
        }

        function initParticles() {
            const canvas = document.getElementById('particles-canvas');
            const ctx = canvas.getContext('2d');
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;

            const particles = [];
            const particleCount = 100;

            class Particle {
                constructor() {
                    this.x = Math.random() * canvas.width;
                    this.y = Math.random() * canvas.height;
                    this.size = Math.random() * 2;
                    this.speedX = Math.random() * 0.5 - 0.25;
                    this.speedY = Math.random() * 0.5 - 0.25;
                    this.opacity = Math.random() * 0.5;
                }

                update() {
                    this.x += this.speedX;
                    this.y += this.speedY;

                    if (this.x > canvas.width) this.x = 0;
                    if (this.x < 0) this.x = canvas.width;
                    if (this.y > canvas.height) this.y = 0;
                    if (this.y < 0) this.y = canvas.height;
                }

                draw() {
                    ctx.fillStyle = `rgba(59, 130, 246, ${this.opacity})`;
                    ctx.beginPath();
                    ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
                    ctx.fill();
                }
            }

            for (let i = 0; i < particleCount; i++) {
                particles.push(new Particle());
            }

            function animate() {
                ctx.clearRect(0, 0, canvas.width, canvas.height);
                
                particles.forEach(particle => {
                    particle.update();
                    particle.draw();
                });

                // Connect particles
                particles.forEach((a, index) => {
                    particles.slice(index + 1).forEach(b => {
                        const dx = a.x - b.x;
                        const dy = a.y - b.y;
                        const distance = Math.sqrt(dx * dx + dy * dy);

                        if (distance < 100) {
                            ctx.strokeStyle = `rgba(59, 130, 246, ${0.1 * (1 - distance / 100)})`;
                            ctx.lineWidth = 0.5;
                            ctx.beginPath();
                            ctx.moveTo(a.x, a.y);
                            ctx.lineTo(b.x, b.y);
                            ctx.stroke();
                        }
                    });
                });

                requestAnimationFrame(animate);
            }

            animate();

            window.addEventListener('resize', () => {
                canvas.width = window.innerWidth;
                canvas.height = window.innerHeight;
            });
        }

        function initCursor() {
            const dot = document.getElementById('cursor-dot');
            const outline = document.getElementById('cursor-outline');

            window.addEventListener('mousemove', (e) => {
                const posX = e.clientX;
                const posY = e.clientY;

                dot.style.left = `${posX}px`;
                dot.style.top = `${posY}px`;

                outline.animate({
                    left: `${posX}px`,
                    top: `${posY}px`
                }, { duration: 500, fill: 'forwards' });
            });

            // Magnetic effect
            document.querySelectorAll('.magnetic-btn').forEach(btn => {
                btn.addEventListener('mouseenter', () => {
                    outline.classList.add('hover');
                });

                btn.addEventListener('mouseleave', () => {
                    outline.classList.remove('hover');
                });

                btn.addEventListener('mousemove', (e) => {
                    const rect = btn.getBoundingClientRect();
                    const x = e.clientX - rect.left - rect.width / 2;
                    const y = e.clientY - rect.top - rect.height / 2;
                    
                    btn.style.transform = `translate(${x * 0.3}px, ${y * 0.3}px)`;
                });

                btn.addEventListener('mouseleave', () => {
                    btn.style.transform = 'translate(0, 0)';
                });
            });
        }

        function initTiltCards() {
            document.querySelectorAll('.tilt-card').forEach(card => {
                card.addEventListener('mousemove', (e) => {
                    const rect = card.getBoundingClientRect();
                    const x = e.clientX - rect.left;
                    const y = e.clientY - rect.top;
                    
                    const centerX = rect.width / 2;
                    const centerY = rect.height / 2;
                    
                    const rotateX = (y - centerY) / 10;
                    const rotateY = (centerX - x) / 10;
                    
                    card.style.transform = `perspective(1000px) rotateX(${rotateX}deg) rotateY(${rotateY}deg) scale3d(1.02, 1.02, 1.02)`;
                });

                card.addEventListener('mouseleave', () => {
                    card.style.transform = 'perspective(1000px) rotateX(0) rotateY(0) scale3d(1, 1, 1)';
                });
            });
        }

        function switchSubject(subjectId) {
            // Update tabs
            document.querySelectorAll('.subject-tab').forEach(tab => {
                tab.classList.remove('tab-active', 'bg-gradient-to-r', 'from-blue-600', 'to-blue-500', 'text-white', 'border-transparent');
                tab.classList.add('bg-white/5', 'text-gray-400', 'border-white/10');
            });
            
            const activeTab = document.querySelector(`[data-subject="${subjectId}"]`);
            activeTab.classList.remove('bg-white/5', 'text-gray-400', 'border-white/10');
            activeTab.classList.add('tab-active', 'bg-gradient-to-r', 'from-blue-600', 'to-blue-500', 'text-white', 'border-transparent');

            // Get data
            const data = subjectsData[subjectId];
            const container = document.getElementById('subject-content');
            
            // Animate out
            container.style.opacity = '0';
            container.style.transform = 'translateY(20px)';
            
            setTimeout(() => {
                // Generate HTML
                let chaptersHtml = '';
                data.chapters.forEach((chapter, index) => {
                    chaptersHtml += `
                        <div class="glass rounded-xl p-6 border border-white/10 hover:border-${data.color}-500/50 transition-all group cursor-pointer transform hover:-translate-y-1">
                            <div class="flex items-start justify-between mb-4">
                                <div class="flex items-center space-x-3">
                                    <span class="w-10 h-10 rounded-full bg-${data.color}-500/20 text-${data.color}-400 flex items-center justify-center text-sm font-bold border border-${data.color}-500/30">${index + 1}</span>
                                    <h4 class="font-bold text-white text-lg group-hover:text-${data.color}-400 transition-colors">${chapter.name}</h4>
                                </div>
                                <i class="fas fa-chevron-right text-gray-600 group-hover:text-${data.color}-400 transition-all group-hover:translate-x-1"></i>
                            </div>
                            <div class="pl-13">
                                <div class="flex flex-wrap gap-2">
                                    ${chapter.topics.map(topic => `<span class="px-3 py-1 bg-white/5 text-gray-400 text-xs rounded-full border border-white/10 group-hover:border-${data.color}-500/30 group-hover:text-${data.color}-300 transition-colors">${topic}</span>`).join('')}
                                </div>
                            </div>
                        </div>
                    `;
                });

                let resourcesHtml = '';
                data.resources.forEach(resource => {
                    let icon = 'fa-file-pdf';
                    let colorClass = 'text-red-400 bg-red-500/20 border-red-500/30';
                    if(resource.type === 'Video') { icon = 'fa-play-circle'; colorClass = 'text-red-400 bg-red-500/20 border-red-500/30'; }
                    if(resource.type === 'Drive') { icon = 'fa-google-drive'; colorClass = 'text-green-400 bg-green-500/20 border-green-500/30'; }
                    if(resource.type === 'Exam') { icon = 'fa-clipboard-list'; colorClass = 'text-blue-400 bg-blue-500/20 border-blue-500/30'; }
                    
                    resourcesHtml += `
                        <a href="${resource.link}" target="_blank" class="flex items-center p-4 rounded-xl border border-white/10 hover:bg-white/5 transition-all group">
                            <div class="w-12 h-12 rounded-lg ${colorClass} flex items-center justify-center mr-4 group-hover:scale-110 transition-transform border">
                                <i class="fas ${icon} text-xl"></i>
                            </div>
                            <div class="flex-1">
                                <h5 class="font-semibold text-white group-hover:text-blue-400 transition-colors">${resource.name}</h5>
                                <span class="text-xs text-gray-500 uppercase tracking-wide">${resource.type}</span>
                            </div>
                            <i class="fas fa-external-link-alt text-gray-600 group-hover:text-blue-400 transition-all group-hover:translate-x-1"></i>
                        </a>
                    `;
                });

                container.innerHTML = `
                    <div class="mb-8">
                        <div class="flex items-center space-x-4 mb-4">
                            <div class="w-16 h-16 rounded-2xl bg-gradient-to-br from-${data.color}-500 to-${data.color}-600 flex items-center justify-center text-3xl text-white shadow-lg">
                                <i class="fas ${data.icon}"></i>
                            </div>
                            <div>
                                <h3 class="text-2xl font-bold text-white">${data.title}</h3>
                                <p class="text-gray-400">${data.description}</p>
                            </div>
                        </div>
                    </div>

                    <div class="grid lg:grid-cols-3 gap-8">
                        <div class="lg:col-span-2">
                            <h4 class="text-lg font-bold text-white mb-6 flex items-center">
                                <i class="fas fa-list-ul mr-2 text-${data.color}-400"></i>
                                Chapter Index
                            </h4>
                            <div class="grid gap-4 max-h-[500px] overflow-y-auto pr-2 custom-scrollbar">
                                ${chaptersHtml}
                            </div>
                        </div>
                        
                        <div class="lg:col-span-1">
                            <h4 class="text-lg font-bold text-white mb-6 flex items-center">
                                <i class="fas fa-download mr-2 text-${data.color}-400"></i>
                                Resources
                            </h4>
                            <div class="space-y-3">
                                ${resourcesHtml}
                            </div>
                            
                            <div class="mt-6 p-6 rounded-xl bg-${data.color}-500/10 border border-${data.color}-500/30">
                                <h5 class="font-semibold text-${data.color}-400 mb-2 flex items-center">
                                    <i class="fas fa-lightbulb mr-2"></i> Study Tip
                                </h5>
                                <p class="text-sm text-gray-400">Focus on examinable knowledge references and practice past papers regularly. Check the official ICAP syllabus for weightage details.</p>
                            </div>
                        </div>
                    </div>
                `;

                // Animate in
                container.style.opacity = '1';
                container.style.transform = 'translateY(0)';
                container.style.transition = 'all 0.5s ease';
            }, 300);
        }

        // Mobile menu toggle
        document.getElementById('mobile-menu-btn').addEventListener('click', () => {
            const menu = document.getElementById('mobile-menu');
            menu.classList.toggle('hidden');
        });

        // Smooth scroll
        document.querySelectorAll('a[href^="#"]').forEach(anchor => {
            anchor.addEventListener('click', function(e) {
                e.preventDefault();
                const target = document.querySelector(this.getAttribute('href'));
                if(target) {
                    target.scrollIntoView({ behavior: 'smooth', block: 'start' });
                    document.getElementById('mobile-menu').classList.add('hidden');
                }
            });
        });

        // Navbar scroll effect
        window.addEventListener('scroll', () => {
            const navbar = document.getElementById('navbar');
            if (window.scrollY > 50) {
                navbar.classList.add('glass-strong');
                navbar.classList.remove('bg-transparent');
            } else {
                navbar.classList.remove('glass-strong');
                navbar.classList.add('bg-transparent');
            }
        });
    </script>
</body>
</html>
