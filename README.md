<!DOCTYPE html>
<html lang="id" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    
    <!-- SEO & Meta Tags (Siap untuk Vercel/GitHub) -->
    <title>Raihanrab | Video & Photo Editor Portfolio</title>
    <meta name="description" content="Portofolio kreatif Raihanrab. Spesialis dalam Video Editing, Color Grading, dan High-end Photo Retouching.">
    <meta name="keywords" content="Video Editor, Photo Editor, Color Grading, Fotografer, Videografer, Portofolio">
    <meta name="author" content="Raihanrab">
    
    <!-- Open Graph / Facebook -->
    <meta property="og:type" content="website">
    <meta property="og:url" content="https://alexvisuals.com/">
    <meta property="og:title" content="Alex Visuals | Cinematic Video & Photo">
    <meta property="og:description" content="Mengubah momen mentah menjadi narasi visual yang memukau dan sinematik.">
    <meta property="og:image" content="https://images.unsplash.com/photo-1522075469751-3a6694fb2f61?q=80&w=1780&auto=format&fit=crop">

    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    
    <!-- Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600&family=Playfair+Display:ital,wght@0,400;0,600;0,700;1,400&display=swap" rel="stylesheet">
    
    <!-- Phosphor Icons -->
    <script src="https://unpkg.com/@phosphor-icons/web"></script>

    <!-- AOS Animation CSS -->
    <link href="https://unpkg.com/aos@2.3.1/dist/aos.css" rel="stylesheet">
    
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                        serif: ['Playfair Display', 'serif'],
                    },
                    colors: {
                        dark: '#050505',
                        darker: '#000000',
                        accent: '#ffffff',
                        muted: '#888888'
                    },
                    animation: {
                        'scrolling-text': 'scrollText 30s linear infinite',
                        'bounce-slow': 'bounce 3s infinite',
                    },
                    keyframes: {
                        scrollText: {
                            '0%': { transform: 'translateX(0)' },
                            '100%': { transform: 'translateX(-50%)' },
                        }
                    }
                }
            }
        }
    </script>
    <style>
        body {
            background-color: theme('colors.dark');
            color: theme('colors.accent');
            overflow-x: hidden;
        }
        
        /* Custom scrollbar */
        ::-webkit-scrollbar { width: 8px; }
        ::-webkit-scrollbar-track { background: theme('colors.darker'); }
        ::-webkit-scrollbar-thumb { background: #333; border-radius: 4px; }
        ::-webkit-scrollbar-thumb:hover { background: #666; }

        /* Glassmorphism utilities */
        .glass {
            background: rgba(255, 255, 255, 0.03);
            backdrop-filter: blur(10px);
            -webkit-backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.05);
        }

        /* Portfolio Item Hover Effects */
        .portfolio-item {
            position: relative;
            overflow: hidden;
            border-radius: 0.75rem;
        }
        .portfolio-item img {
            transition: transform 0.7s cubic-bezier(0.4, 0, 0.2, 1);
        }
        .portfolio-item:hover img {
            transform: scale(1.05);
        }
        .portfolio-overlay {
            position: absolute;
            inset: 0;
            background: linear-gradient(to top, rgba(0,0,0,0.95) 0%, rgba(0,0,0,0.4) 50%, transparent 100%);
            opacity: 0;
            transition: all 0.4s ease;
            display: flex;
            flex-direction: column;
            justify-content: flex-end;
            padding: 2rem;
            transform: translateY(10px);
        }
        .portfolio-item:hover .portfolio-overlay {
            opacity: 1;
            transform: translateY(0);
        }

        /* Subtle Background Glow */
        .glow-circle {
            position: absolute;
            border-radius: 50%;
            background: radial-gradient(circle, rgba(255,255,255,0.08) 0%, rgba(0,0,0,0) 70%);
            filter: blur(60px);
            z-index: -1;
            pointer-events: none;
        }

        /* Play Button Overlay for Videos */
        .play-btn {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%) scale(0.8);
            opacity: 0;
            transition: all 0.4s ease;
            background: rgba(255,255,255,0.2);
            backdrop-filter: blur(5px);
            border-radius: 50%;
            width: 60px;
            height: 60px;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        .portfolio-item:hover .play-btn {
            opacity: 1;
            transform: translate(-50%, -50%) scale(1);
        }
    </style>
</head>
<body class="antialiased selection:bg-white selection:text-black relative">

    <!-- Background decorative glows -->
    <div class="glow-circle w-[500px] h-[500px] top-0 left-0 -translate-x-1/2 -translate-y-1/2"></div>
    <div class="glow-circle w-[600px] h-[600px] bottom-0 right-0 translate-x-1/3 translate-y-1/3"></div>

    <nav class="fixed w-full z-50 top-0 transition-all duration-300" id="navbar">
        <div class="max-w-7xl mx-auto px-6 py-5 flex justify-between items-center">
            <a href="#" class="font-serif text-2xl font-bold tracking-wider z-50 relative group">
                ALEX<span class="text-muted font-sans font-light text-sm ml-1 group-hover:text-white transition-colors">VISUALS</span>
            </a>
            
            <!-- Desktop Menu -->
            <div class="hidden md:flex space-x-10 text-xs uppercase tracking-[0.2em] font-medium text-muted">
                <a href="#home" class="hover:text-white transition-colors">Home</a>
                <a href="#services" class="hover:text-white transition-colors">Services</a>
                <a href="#work" class="hover:text-white transition-colors">Work</a>
                <a href="#about" class="hover:text-white transition-colors">About</a>
            </div>

            <div class="hidden md:block">
                <a href="#contact" class="text-xs uppercase tracking-widest border border-white/20 px-5 py-2 rounded-full hover:bg-white hover:text-black transition-all">Let's Talk</a>
            </div>

            <!-- Mobile Menu Button -->
            <button id="mobile-menu-btn" class="md:hidden text-white z-50 relative p-2 focus:outline-none">
                <i class="ph ph-list text-2xl" id="menu-icon"></i>
            </button>
        </div>

        <!-- Mobile Menu Overlay -->
        <div id="mobile-menu" class="fixed inset-0 bg-darker/95 backdrop-blur-xl flex flex-col justify-center items-center opacity-0 pointer-events-none transition-all duration-500 z-40">
            <div class="flex flex-col space-y-8 text-center text-3xl font-serif">
                <a href="#home" class="mobile-link hover:text-muted transition-colors transform translate-y-4 opacity-0">Home</a>
                <a href="#services" class="mobile-link hover:text-muted transition-colors transform translate-y-4 opacity-0">Services</a>
                <a href="#work" class="mobile-link hover:text-muted transition-colors transform translate-y-4 opacity-0">Work</a>
                <a href="#about" class="mobile-link hover:text-muted transition-colors transform translate-y-4 opacity-0">About</a>
                <a href="#contact" class="mobile-link text-lg font-sans border-b border-white/30 pb-1 mt-4 transform translate-y-4 opacity-0">Let's Talk</a>
            </div>
        </div>
    </nav>

    <section id="home" class="relative min-h-screen flex flex-col items-center justify-center px-6 pt-20">
        <div class="text-center z-10 max-w-5xl mx-auto w-full">
            <div data-aos="fade-down" data-aos-duration="1000">
                <p class="text-muted uppercase tracking-[0.4em] text-xs md:text-sm mb-6 flex items-center justify-center gap-3">
                    <span class="w-8 h-[1px] bg-muted"></span>
                    Director & Editor
                    <span class="w-8 h-[1px] bg-muted"></span>
                </p>
            </div>
            
            <h1 class="text-5xl md:text-7xl lg:text-8xl font-serif font-bold mb-6 leading-[1.1]" data-aos="fade-up" data-aos-duration="1000" data-aos-delay="200">
                Crafting <span class="italic text-transparent bg-clip-text bg-gradient-to-r from-gray-300 via-gray-500 to-gray-700">Visual</span><br>
                Narratives.
            </h1>
            
            <p class="text-base md:text-xl text-muted max-w-2xl mx-auto mb-12 font-light leading-relaxed" data-aos="fade-up" data-aos-duration="1000" data-aos-delay="400">
                Mengubah rekaman mentah menjadi mahakarya sinematik. Menyampaikan pesan dan emosi melalui ritme editing dan pewarnaan yang presisi.
            </p>
            
            <div data-aos="fade-up" data-aos-duration="1000" data-aos-delay="600">
                <a href="#work" class="inline-flex items-center space-x-3 bg-white text-black px-8 py-4 rounded-full hover:bg-gray-200 transition-all duration-300 group font-medium">
                    <span class="text-sm uppercase tracking-widest">Eksplorasi Karya</span>
                    <i class="ph ph-arrow-right group-hover:translate-x-1 transition-transform"></i>
                </a>
            </div>
        </div>
        
        <!-- Scroll Down Indicator -->
        <div class="absolute bottom-10 left-1/2 -translate-x-1/2 flex flex-col items-center gap-2 opacity-50 hover:opacity-100 transition-opacity cursor-pointer animate-bounce-slow" onclick="document.getElementById('services').scrollIntoView()">
            <span class="text-[10px] uppercase tracking-widest">Scroll</span>
            <div class="w-[1px] h-12 bg-gradient-to-b from-white to-transparent"></div>
        </div>
    </section>

    <section class="py-10 border-y border-white/5 bg-white/[0.01] overflow-hidden flex whitespace-nowrap relative">
        <!-- Fade edges -->
        <div class="absolute inset-y-0 left-0 w-32 bg-gradient-to-r from-dark to-transparent z-10"></div>
        <div class="absolute inset-y-0 right-0 w-32 bg-gradient-to-l from-dark to-transparent z-10"></div>
        
        <div class="animate-scrolling-text flex items-center space-x-16 md:space-x-32 px-8">
            <!-- Simulated Client Logos using text for demo -->
            <div class="text-2xl font-serif text-white/30 uppercase tracking-widest font-bold">Vogue</div>
            <div class="text-2xl font-serif text-white/30 uppercase tracking-widest font-bold">Nike</div>
            <div class="text-2xl font-serif text-white/30 uppercase tracking-widest font-bold">Sony Music</div>
            <div class="text-2xl font-serif text-white/30 uppercase tracking-widest font-bold">Netflix</div>
            <div class="text-2xl font-serif text-white/30 uppercase tracking-widest font-bold">Red Bull</div>
            
            <!-- Duplicate for infinite loop -->
            <div class="text-2xl font-serif text-white/30 uppercase tracking-widest font-bold">Vogue</div>
            <div class="text-2xl font-serif text-white/30 uppercase tracking-widest font-bold">Nike</div>
            <div class="text-2xl font-serif text-white/30 uppercase tracking-widest font-bold">Sony Music</div>
            <div class="text-2xl font-serif text-white/30 uppercase tracking-widest font-bold">Netflix</div>
            <div class="text-2xl font-serif text-white/30 uppercase tracking-widest font-bold">Red Bull</div>
        </div>
    </section>

    <section id="services" class="py-24 px-6">
        <div class="max-w-7xl mx-auto">
            <div class="mb-16 text-center" data-aos="fade-up">
                <h2 class="text-3xl md:text-5xl font-serif font-bold mb-4">Keahlian Utama</h2>
                <p class="text-muted max-w-2xl mx-auto">Pendekatan komprehensif dalam pasca-produksi untuk memastikan visual Anda mencapai potensi maksimalnya.</p>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                <!-- Service 1 -->
                <div class="glass p-8 rounded-2xl hover:-translate-y-2 transition-transform duration-300 group" data-aos="fade-up" data-aos-delay="100">
                    <i class="ph ph-scissors text-4xl text-gray-400 mb-6 group-hover:text-white transition-colors"></i>
                    <h3 class="text-xl font-bold mb-3">Offline & Online Editing</h3>
                    <p class="text-muted text-sm leading-relaxed">Merangkai cerita dari footage mentah, mengatur ritme (pacing), dan mengunci susunan akhir untuk TVC, dokumenter, atau video musik.</p>
                </div>
                <!-- Service 2 -->
                <div class="glass p-8 rounded-2xl hover:-translate-y-2 transition-transform duration-300 group" data-aos="fade-up" data-aos-delay="200">
                    <i class="ph ph-palette text-4xl text-gray-400 mb-6 group-hover:text-white transition-colors"></i>
                    <h3 class="text-xl font-bold mb-3">Color Grading</h3>
                    <p class="text-muted text-sm leading-relaxed">Menciptakan "look" dan "mood" yang spesifik (sinematik, komersial, vintage) menggunakan DaVinci Resolve untuk memandu emosi penonton.</p>
                </div>
                <!-- Service 3 -->
                <div class="glass p-8 rounded-2xl hover:-translate-y-2 transition-transform duration-300 group" data-aos="fade-up" data-aos-delay="300">
                    <i class="ph ph-magic-wand text-4xl text-gray-400 mb-6 group-hover:text-white transition-colors"></i>
                    <h3 class="text-xl font-bold mb-3">High-end Retouching</h3>
                    <p class="text-muted text-sm leading-relaxed">Penyempurnaan detail foto untuk editorial fashion dan komersial, termasuk skin retouching presisi tanpa menghilangkan tekstur alami.</p>
                </div>
            </div>
        </div>
    </section>

    <section id="work" class="py-24 px-6 bg-white/[0.02] border-y border-white/5">
        <div class="max-w-7xl mx-auto">
            <div class="flex flex-col md:flex-row justify-between items-end mb-12 gap-8" data-aos="fade-up">
                <div>
                    <h2 class="text-4xl md:text-5xl font-serif font-bold mb-4">Selected Works</h2>
                    <p class="text-muted">Karya pilihan dari kolaborasi terbaru.</p>
                </div>
                
                <!-- Filters -->
                <div class="flex flex-wrap gap-2" id="portfolio-filters">
                    <button class="filter-btn active px-5 py-2 rounded-full bg-white text-black text-xs uppercase tracking-wider font-semibold transition-all" data-filter="all">Semua</button>
                    <button class="filter-btn px-5 py-2 rounded-full border border-white/20 text-white hover:bg-white/10 text-xs uppercase tracking-wider font-semibold transition-all" data-filter="video">Video</button>
                    <button class="filter-btn px-5 py-2 rounded-full border border-white/20 text-white hover:bg-white/10 text-xs uppercase tracking-wider font-semibold transition-all" data-filter="photo">Foto</button>
                </div>
            </div>

            <!-- Portfolio Grid -->
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6" id="portfolio-grid">
                
                <!-- Item 1: Video (Besar) -->
                <div class="portfolio-item group h-96 md:col-span-2" data-category="video" data-aos="fade-up">
                    <img src="https://images.unsplash.com/photo-1536240478700-b869070f9279?q=80&w=2000&auto=format&fit=crop" alt="The Silent Ocean - Mini Doc" class="w-full h-full object-cover object-center">
                    <div class="play-btn">
                        <i class="ph-fill ph-play text-white text-2xl"></i>
                    </div>
                    <div class="portfolio-overlay">
                         <div class="flex items-center gap-2 mb-3">
                            <span class="glass text-[10px] uppercase tracking-widest px-3 py-1 rounded-full text-white flex items-center gap-1"><i class="ph ph-video-camera"></i> Documentary</span>
                        </div>
                        <h3 class="text-3xl font-serif font-bold mb-2">The Silent Ocean</h3>
                        <p class="text-sm text-gray-300">Lead Editor & Colorist • 2023</p>
                    </div>
                </div>

                <!-- Item 2: Photo -->
                <div class="portfolio-item group h-96" data-category="photo" data-aos="fade-up" data-aos-delay="100">
                    <img src="https://images.unsplash.com/photo-1542038784456-1ea8e935640e?q=80&w=2070&auto=format&fit=crop" alt="Fashion Editorial" class="w-full h-full object-cover">
                    <div class="portfolio-overlay">
                        <div class="flex items-center gap-2 mb-3">
                            <span class="glass text-[10px] uppercase tracking-widest px-3 py-1 rounded-full text-white flex items-center gap-1"><i class="ph ph-camera"></i> Editorial</span>
                        </div>
                        <h3 class="text-2xl font-serif font-bold mb-2">Neon Nights</h3>
                        <p class="text-sm text-gray-300">Retouching & Grading</p>
                    </div>
                </div>

                <!-- Item 3: Photo -->
                <div class="portfolio-item group h-80" data-category="photo" data-aos="fade-up">
                    <img src="https://images.unsplash.com/photo-1534528741775-53994a69daeb?q=80&w=1964&auto=format&fit=crop" alt="Portrait" class="w-full h-full object-cover object-top">
                    <div class="portfolio-overlay">
                         <div class="flex items-center gap-2 mb-3">
                            <span class="glass text-[10px] uppercase tracking-widest px-3 py-1 rounded-full text-white flex items-center gap-1"><i class="ph ph-camera"></i> Portrait</span>
                        </div>
                        <h3 class="text-xl font-serif font-bold mb-2">Raw Human Series</h3>
                        <p class="text-sm text-gray-300">Skin Retouching</p>
                    </div>
                </div>

                <!-- Item 4: Video -->
                <div class="portfolio-item group h-80" data-category="video" data-aos="fade-up" data-aos-delay="100">
                    <img src="https://images.unsplash.com/photo-1492691527719-9d1e07e534b4?q=80&w=2071&auto=format&fit=crop" alt="Cinematic Commercial" class="w-full h-full object-cover">
                    <div class="play-btn">
                        <i class="ph-fill ph-play text-white text-2xl"></i>
                    </div>
                    <div class="portfolio-overlay">
                        <div class="flex items-center gap-2 mb-3">
                            <span class="glass text-[10px] uppercase tracking-widest px-3 py-1 rounded-full text-white flex items-center gap-1"><i class="ph ph-video-camera"></i> Commercial</span>
                        </div>
                        <h3 class="text-xl font-serif font-bold mb-2">Urban Lifestyle TVC</h3>
                        <p class="text-sm text-gray-300">Editing & Color Grading</p>
                    </div>
                </div>

                <!-- Item 5: Video -->
                <div class="portfolio-item group h-80" data-category="video" data-aos="fade-up" data-aos-delay="200">
                    <img src="https://images.unsplash.com/photo-1574717024653-61fd2cf4d44d?q=80&w=2070&auto=format&fit=crop" alt="Music Video" class="w-full h-full object-cover">
                    <div class="play-btn">
                        <i class="ph-fill ph-play text-white text-2xl"></i>
                    </div>
                    <div class="portfolio-overlay">
                         <div class="flex items-center gap-2 mb-3">
                            <span class="glass text-[10px] uppercase tracking-widest px-3 py-1 rounded-full text-white flex items-center gap-1"><i class="ph ph-video-camera"></i> Music Video</span>
                        </div>
                        <h3 class="text-xl font-serif font-bold mb-2">"Echoes" - Official MV</h3>
                        <p class="text-sm text-gray-300">Offline Editing</p>
                    </div>
                </div>

            </div>
        </div>
    </section>

    <section id="about" class="py-32 px-6 relative">
        <div class="max-w-6xl mx-auto flex flex-col md:flex-row items-center gap-16 lg:gap-24">
            <div class="w-full md:w-1/2 relative" data-aos="fade-right">
                <!-- Image decoration -->
                <div class="absolute -top-6 -left-6 w-32 h-32 border-t-2 border-l-2 border-white/20"></div>
                <div class="absolute -bottom-6 -right-6 w-32 h-32 border-b-2 border-r-2 border-white/20"></div>
                
                <div class="relative z-10 rounded-xl overflow-hidden grayscale hover:grayscale-0 transition-all duration-700 shadow-2xl">
                    <img src="https://images.unsplash.com/photo-1522075469751-3a6694fb2f61?q=80&w=1780&auto=format&fit=crop" alt="Alex Visuals Editor" class="w-full h-[600px] object-cover">
                </div>
            </div>
            
            <div class="w-full md:w-1/2" data-aos="fade-left">
                <p class="text-white/50 uppercase tracking-widest text-xs mb-4">Tentang Saya</p>
                <h2 class="text-4xl md:text-5xl font-serif font-bold mb-8">Cerita di Balik Lensa & Timeline.</h2>
                
                <div class="space-y-6 text-muted font-light leading-relaxed mb-10 text-lg">
                    <p>
                        Halo, saya Alex. Editor video dan *retoucher* foto yang berbasis di Jakarta dengan lebih dari 7 tahun pengalaman menghidupkan visi kreatif brand dan musisi.
                    </p>
                    <p>
                        Filosofi saya sederhana: <strong class="text-white font-normal">Teknik yang sempurna harus tunduk pada cerita.</strong> Tidak peduli seberapa rumit efek visual atau gradasi warnanya, jika tidak membangkitkan emosi, maka itu belum selesai.
                    </p>
                </div>
                
                <div class="grid grid-cols-2 gap-8 border-t border-white/10 pt-8">
                    <div>
                        <h4 class="font-semibold text-white mb-3 text-sm uppercase tracking-wider flex items-center gap-2"><i class="ph ph-monitor-play"></i> Software</h4>
                        <ul class="text-sm text-muted space-y-2">
                            <li>Adobe Premiere Pro</li>
                            <li>DaVinci Resolve Studio</li>
                            <li>Adobe After Effects</li>
                            <li>Adobe Photoshop</li>
                        </ul>
                    </div>
                    <div>
                        <h4 class="font-semibold text-white mb-3 text-sm uppercase tracking-wider flex items-center gap-2"><i class="ph ph-award"></i> Pencapaian</h4>
                        <ul class="text-sm text-muted space-y-2">
                            <li><span class="text-white">100+</span> Proyek Komersial</li>
                            <li><span class="text-white">50M+</span> Views di YouTube</li>
                            <li>Best Editor Indovidfest '22</li>
                        </ul>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <section id="contact" class="py-32 px-6 bg-darker relative overflow-hidden">
        <!-- Abstract gradient blob -->
        <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-[800px] h-[800px] bg-white/[0.02] rounded-full blur-3xl -z-10"></div>
        
        <div class="max-w-4xl mx-auto text-center z-10 relative" data-aos="zoom-in">
            <h2 class="text-5xl md:text-7xl font-serif font-bold mb-6">Mari Berkolaborasi.</h2>
            <p class="text-muted mb-12 text-xl max-w-2xl mx-auto">Punya proyek yang membutuhkan sentuhan magis di ruang editing? Saya siap membantu mewujudkan visi Anda.</p>
            
            <a href="mailto:hello@alexvisuals.com" class="inline-block text-3xl md:text-5xl font-serif hover:italic transition-all border-b-2 border-white/30 hover:border-white pb-2 mb-16">
                hello@alexvisuals.com
            </a>

            <div class="flex justify-center space-x-4">
                <a href="#" class="text-gray-400 hover:text-white hover:-translate-y-1 transition-all p-4 glass rounded-full" aria-label="Instagram">
                    <i class="ph ph-instagram-logo text-2xl"></i>
                </a>
                <a href="#" class="text-gray-400 hover:text-white hover:-translate-y-1 transition-all p-4 glass rounded-full" aria-label="Behance">
                    <i class="ph ph-behance-logo text-2xl"></i>
                </a>
                <a href="#" class="text-gray-400 hover:text-white hover:-translate-y-1 transition-all p-4 glass rounded-full" aria-label="Vimeo">
                    <i class="ph ph-vimeo-logo text-2xl"></i>
                </a>
                <a href="#" class="text-gray-400 hover:text-white hover:-translate-y-1 transition-all p-4 glass rounded-full" aria-label="LinkedIn">
                    <i class="ph ph-linkedin-logo text-2xl"></i>
                </a>
            </div>
        </div>
    </section>

    <footer class="py-8 text-center text-xs uppercase tracking-widest text-gray-600 bg-darker border-t border-white/5 flex flex-col md:flex-row justify-center items-center gap-4">
        <p>&copy; <span id="year"></span> Alex Visuals. All rights reserved.</p>
        <span class="hidden md:block text-gray-800">|</span>
        <p>Designed with <i class="ph-fill ph-heart text-white/30 mx-1"></i> in Jakarta</p>
    </footer>

    <!-- AOS Script -->
    <script src="https://unpkg.com/aos@2.3.1/dist/aos.js"></script>
    
    <script>
        document.addEventListener('DOMContentLoaded', () => {
            // Initialize AOS Animation
            AOS.init({
                duration: 800,
                easing: 'ease-out-cubic',
                once: true,
                offset: 50
            });

            // Set current year in footer
            document.getElementById('year').textContent = new Date().getFullYear();

            // Navbar scroll effect (Glassmorphism)
            const navbar = document.getElementById('navbar');
            window.addEventListener('scroll', () => {
                if (window.scrollY > 50) {
                    navbar.classList.add('glass', 'py-3');
                    navbar.classList.remove('py-5', 'border-transparent');
                } else {
                    navbar.classList.remove('glass', 'py-3');
                    navbar.classList.add('py-5');
                }
            });

            // Mobile Menu Logic with staggered animations
            const mobileMenuBtn = document.getElementById('mobile-menu-btn');
            const mobileMenu = document.getElementById('mobile-menu');
            const menuIcon = document.getElementById('menu-icon');
            const mobileLinks = document.querySelectorAll('.mobile-link');
            let isMenuOpen = false;

            function toggleMenu() {
                isMenuOpen = !isMenuOpen;
                if (isMenuOpen) {
                    mobileMenu.classList.remove('opacity-0', 'pointer-events-none');
                    mobileMenu.classList.add('opacity-100', 'pointer-events-auto');
                    menuIcon.classList.remove('ph-list');
                    menuIcon.classList.add('ph-x');
                    document.body.style.overflow = 'hidden'; 
                    
                    // Staggered link animation
                    mobileLinks.forEach((link, index) => {
                        setTimeout(() => {
                            link.classList.remove('translate-y-4', 'opacity-0');
                        }, 100 * (index + 1));
                    });
                } else {
                    mobileMenu.classList.add('opacity-0', 'pointer-events-none');
                    mobileMenu.classList.remove('opacity-100', 'pointer-events-auto');
                    menuIcon.classList.remove('ph-x');
                    menuIcon.classList.add('ph-list');
                    document.body.style.overflow = '';
                    
                    // Reset link animation
                    mobileLinks.forEach(link => {
                        link.classList.add('translate-y-4', 'opacity-0');
                    });
                }
            }

            mobileMenuBtn.addEventListener('click', toggleMenu);

            mobileLinks.forEach(link => {
                link.addEventListener('click', () => {
                    if (isMenuOpen) toggleMenu();
                });
            });

            // Enhanced Portfolio Filtering
            const filterBtns = document.querySelectorAll('.filter-btn');
            const portfolioItems = document.querySelectorAll('.portfolio-item');

            filterBtns.forEach(btn => {
                btn.addEventListener('click', () => {
                    // Update active styling
                    filterBtns.forEach(b => {
                        b.classList.remove('active', 'bg-white', 'text-black');
                        b.classList.add('border-white/20', 'text-white', 'hover:bg-white/10');
                    });
                    btn.classList.add('active', 'bg-white', 'text-black');
                    btn.classList.remove('border-white/20', 'text-white', 'hover:bg-white/10');

                    const filterValue = btn.getAttribute('data-filter');

                    portfolioItems.forEach(item => {
                        // Reset AOS for filtering
                        item.removeAttribute('data-aos');
                        item.classList.remove('aos-init', 'aos-animate');

                        if (filterValue === 'all' || item.getAttribute('data-category') === filterValue) {
                            item.style.display = 'block';
                            setTimeout(() => {
                                item.style.opacity = '1';
                                item.style.transform = 'scale(1)';
                            }, 50);
                        } else {
                            item.style.opacity = '0';
                            item.style.transform = 'scale(0.95)';
                            setTimeout(() => {
                                item.style.display = 'none';
                            }, 400); // match transition duration
                        }
                    });
                });
            });
        });
    </script>
</body>
</html>
