<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Yayasan Tangan Kasih - Media Pembelajaran Interaktif</title>

    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    
    <!-- Google Fonts: Fredoka & Poppins -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Fredoka:wght@400;500;600;700&family=Poppins:wght@400;500;600;700&display=swap" rel="stylesheet">
    
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <!-- Chart.js for Admin Analytics -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        brand: {
                            blue: '#4A90E2',
                            yellow: '#FFD166',
                            green: '#06D6A0',
                            coral: '#FF6B6B',
                            purple: '#A29BFE',
                            bg: '#F4F7FE'
                        }
                    },
                    fontFamily: {
                        fredoka: ['Fredoka', 'sans-serif'],
                        poppins: ['Poppins', 'sans-serif']
                    }
                }
            }
        }
    </script>

    <style>
        body {
            font-family: 'Poppins', sans-serif;
            background-color: #F4F7FE;
        }
        h1, h2, h3, h4, .font-fun {
            font-family: 'Fredoka', cursive, sans-serif;
        }
        .bouncy-hover:hover {
            transform: translateY(-4px) scale(1.02);
            transition: all 0.2s ease-in-out;
        }
        .custom-scrollbar::-webkit-scrollbar {
            width: 6px;
        }
        .custom-scrollbar::-webkit-scrollbar-track {
            background: #f1f1f1;
            border-radius: 10px;
        }
        .custom-scrollbar::-webkit-scrollbar-thumb {
            background: #cbd5e1;
            border-radius: 10px;
        }
        .pulse-star {
            animation: pulse 1.5s infinite;
        }
        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.15); }
        }
    </style>
</head>
<body class="min-h-screen flex flex-col text-slate-800">

    <!-- HEADER / NAVIGATION -->
    <header class="bg-white shadow-md sticky top-0 z-50 transition-all">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex items-center justify-between h-20">
                <!-- Branding -->
                <div class="flex items-center space-x-3 cursor-pointer" onclick="switchView('dashboard')">
                    <div class="w-12 h-12 bg-gradient-to-tr from-brand-coral to-brand-yellow rounded-2xl flex items-center justify-center text-white shadow-lg shadow-coral-200">
                        <i class="fa-solid font-bold fa-heart-pulse text-2xl"></i>
                    </div>
                    <div>
                        <span class="font-fun font-bold text-2xl text-slate-800 tracking-wide block leading-none">Tangan Kasih</span>
                        <span class="text-xs font-semibold text-brand-blue tracking-wider uppercase">Belajar & Tumbuh Bersama</span>
                    </div>
                </div>

                <!-- Main Nav Links -->
                <nav class="hidden md:flex space-x-2 bg-slate-100 p-1.5 rounded-2xl">
                    <button onclick="switchView('dashboard')" id="nav-dashboard" class="nav-btn px-5 py-2.5 rounded-xl font-fun font-semibold text-sm transition-all bg-white text-brand-blue shadow-sm">
                        <i class="fa-solid fa-house mr-2"></i>Beranda Belajar
                    </button>
                    <button onclick="switchView('recommendations')" id="nav-recommendations" class="nav-btn px-5 py-2.5 rounded-xl font-fun font-semibold text-sm text-slate-600 hover:text-brand-blue transition-all">
                        <i class="fa-solid fa-wand-magic-sparkles mr-2 text-brand-yellow"></i>Rekomendasi Pintar
                    </button>
                    <button onclick="switchView('admin')" id="nav-admin" class="nav-btn px-5 py-2.5 rounded-xl font-fun font-semibold text-sm text-slate-600 hover:text-brand-blue transition-all">
                        <i class="fa-solid fa-chart-line mr-2 text-brand-purple"></i>Portal Relawan
                    </button>
                </nav>

                <!-- Profile & Rewards Widget -->
                <div class="flex items-center space-x-4">
                    <!-- Stars Counter -->
                    <div class="flex items-center bg-amber-50 border border-amber-200 px-4 py-2 rounded-2xl shadow-sm">
                        <i class="fa-solid fa-star text-amber-400 text-xl mr-2 pulse-star"></i>
                        <div>
                            <div class="text-[10px] text-amber-700 uppercase font-bold leading-none">Bintangku</div>
                            <div id="user-stars" class="font-fun font-bold text-lg text-amber-800 leading-none">120</div>
                        </div>
                    </div>

                    <!-- Profile Switcher Dropdown -->
                    <div class="relative group">
                        <div class="flex items-center space-x-2 bg-slate-50 border border-slate-200 p-1.5 pr-3 rounded-2xl cursor-pointer hover:bg-slate-100 transition-all">
                            <img id="user-avatar" src="https://api.dicebear.com/7.x/bottts/svg?seed=Budi" alt="Avatar" class="w-10 h-10 rounded-xl bg-brand-blue/20">
                            <div class="hidden sm:block text-left">
                                <div id="user-name" class="font-fun font-bold text-sm text-slate-700 leading-none">Budi</div>
                                <div id="user-level" class="text-[11px] text-slate-500 font-medium">Level 1 - Pemula</div>
                            </div>
                            <i class="fa-solid fa-chevron-down text-xs text-slate-400 ml-1"></i>
                        </div>

                        <!-- Dropdown Menu -->
                        <div class="absolute right-0 mt-2 w-56 bg-white rounded-2xl shadow-xl border border-slate-100 py-2 hidden group-hover:block z-50">
                            <div class="px-4 py-2 border-b border-slate-100 text-xs font-semibold text-slate-400 uppercase">Pilih Profil Anak</div>
                            <button onclick="selectUser('budi')" class="w-full text-left px-4 py-2.5 hover:bg-slate-50 flex items-center space-x-3 transition-colors">
                                <img src="https://api.dicebear.com/7.x/bottts/svg?seed=Budi" class="w-8 h-8 rounded-lg bg-blue-100">
                                <div>
                                    <div class="font-bold text-sm text-slate-700">Budi</div>
                                    <div class="text-xs text-slate-400">Level 1 (Pemula)</div>
                                </div>
                            </button>
                            <button onclick="selectUser('siti')" class="w-full text-left px-4 py-2.5 hover:bg-slate-50 flex items-center space-x-3 transition-colors">
                                <img src="https://api.dicebear.com/7.x/bottts/svg?seed=Siti" class="w-8 h-8 rounded-lg bg-pink-100">
                                <div>
                                    <div class="font-bold text-sm text-slate-700">Siti</div>
                                    <div class="text-xs text-slate-400">Level 2 (Menengah)</div>
                                </div>
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </header>

    <!-- Navigasi mobile -->
    <nav class="md:hidden bg-white border-b border-slate-100 flex justify-around p-2 text-xs font-fun font-semibold text-slate-600">
        <button onclick="switchView('dashboard')" class="px-3 py-2"><i class="fa-solid fa-house mr-1"></i>Beranda</button>
        <button onclick="switchView('recommendations')" class="px-3 py-2"><i class="fa-solid fa-wand-magic-sparkles mr-1 text-brand-yellow"></i>Rekomendasi</button>
        <button onclick="switchView('admin')" class="px-3 py-2"><i class="fa-solid fa-chart-line mr-1 text-brand-purple"></i>Relawan</button>
    </nav>

    <!-- MAIN CONTENT CONTAINER -->
    <main class="flex-grow max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-8">

        <!-- VIEW 1: DASHBOARD PEMBELAJARAN (UTAMA) -->
        <section id="view-dashboard" class="space-y-8">
            <!-- Welcome Banner -->
            <div class="bg-gradient-to-r from-brand-blue via-indigo-500 to-brand-purple rounded-3xl p-6 sm:p-8 text-white shadow-xl relative overflow-hidden flex flex-col md:flex-row items-center justify-between">
                <div class="z-10 max-w-xl text-center md:text-left space-y-3">
                    <span class="bg-white/20 text-white text-xs font-bold px-3 py-1 rounded-full uppercase tracking-wider backdrop-blur-sm inline-block">
                        <i class="fa-solid fa-sparkles mr-1"></i> Yayasan Tangan Kasih
                    </span>
                    <h1 class="text-3xl sm:text-4xl font-bold leading-tight">Halo, <span id="banner-user-name">Budi</span>! 👋</h1>
                    <p class="text-blue-100 text-sm sm:text-base font-medium">
                        Siap untuk petualangan seru hari ini? Pilih materi favoritmu atau ikuti saran pembelajaran pintar di bawah ini!
                    </p>
                    <div class="pt-2 flex flex-wrap gap-3 justify-center md:justify-start">
                        <button onclick="scrollToRecommendations()" class="bg-brand-yellow text-slate-900 font-fun font-bold px-5 py-2.5 rounded-2xl hover:bg-amber-300 transition-all shadow-md flex items-center">
                            <i class="fa-solid fa-compass mr-2"></i>Lihat Rekomendasi
                        </button>
                    </div>
                </div>
                <div class="relative mt-6 md:mt-0 z-10 flex justify-center">
                    <div class="w-40 h-40 sm:w-48 sm:h-48 bg-white/10 backdrop-blur-md rounded-full border-4 border-white/30 flex items-center justify-center relative shadow-inner">
                        <i class="fa-solid fa-rocket text-7xl text-brand-yellow animate-bounce"></i>
                    </div>
                </div>
                <!-- Background decoration shapes -->
                <div class="absolute -right-10 -top-10 w-48 h-48 bg-white/10 rounded-full blur-2xl"></div>
                <div class="absolute -left-10 -bottom-10 w-48 h-48 bg-brand-yellow/20 rounded-full blur-2xl"></div>
            </div>

            <!-- SMART RECOMMENDATIONS SECTION -->
            <div id="recommendation-section" class="space-y-4">
                <div class="flex items-center justify-between">
                    <div class="flex items-center space-x-3">
                        <div class="w-10 h-10 bg-amber-100 rounded-xl flex items-center justify-center text-amber-600">
                            <i class="fa-solid fa-wand-magic-sparkles text-xl"></i>
                        </div>
                        <div>
                            <h2 class="text-2xl font-bold text-slate-800">Rekomendasi Khusus Untukmu</h2>
                            <p class="text-xs text-slate-500">Disesuaikan berdasarkan kemampuan & riwayat kuis kamu</p>
                        </div>
                    </div>
                </div>

                <!-- Recommendation Cards Container (Populated by JS) -->
                <div id="recommendation-cards-container" class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <!-- Dynamic Recommendation Cards will be injected here -->
                </div>
            </div>

            <!-- ALL MODULES SECTION WITH FILTER -->
            <div class="space-y-6 pt-4">
                <div class="flex flex-col md:flex-row md:items-center justify-between gap-4">
                    <div class="flex items-center space-x-3">
                        <div class="w-10 h-10 bg-blue-100 rounded-xl flex items-center justify-center text-brand-blue">
                            <i class="fa-solid fa-book-open text-xl"></i>
                        </div>
                        <h2 class="text-2xl font-bold text-slate-800">Semua Modul Belajar</h2>
                    </div>

                    <!-- Filter Category Buttons -->
                    <div class="flex flex-wrap gap-2 bg-slate-200/60 p-1.5 rounded-2xl">
                        <button onclick="filterModules('all', this)" class="filter-btn active bg-white text-brand-blue shadow-sm font-fun text-xs font-bold px-4 py-2 rounded-xl transition-all">Semua</button>
                        <button onclick="filterModules('Matematika', this)" class="filter-btn text-slate-600 font-fun text-xs font-bold px-4 py-2 rounded-xl transition-all hover:text-brand-blue">Matematika</button>
                        <button onclick="filterModules('Bahasa', this)" class="filter-btn text-slate-600 font-fun text-xs font-bold px-4 py-2 rounded-xl transition-all hover:text-brand-blue">Bahasa</button>
                        <button onclick="filterModules('Sains', this)" class="filter-btn text-slate-600 font-fun text-xs font-bold px-4 py-2 rounded-xl transition-all hover:text-brand-blue">Sains</button>
                        <button onclick="filterModules('Karakter', this)" class="filter-btn text-slate-600 font-fun text-xs font-bold px-4 py-2 rounded-xl transition-all hover:text-brand-blue">Karakter</button>
                    </div>
                </div>

                <!-- Modules Grid -->
                <div id="modules-grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6">
                    <!-- Dynamic Modules inserted via JS -->
                </div>
            </div>
        </section>

        <!-- VIEW 2: MODUL INTERAKTIF & KUIS (LEARNING PLAYER) -->
        <section id="view-module" class="hidden space-y-6">
            <button onclick="switchView('dashboard')" class="inline-flex items-center text-slate-600 hover:text-brand-blue font-fun font-bold text-sm bg-white border border-slate-200 px-4 py-2 rounded-xl shadow-sm transition-all hover:shadow-md">
                <i class="fa-solid fa-arrow-left mr-2"></i>Kembali ke Beranda
            </button>

            <div class="bg-white rounded-3xl border border-slate-100 shadow-xl overflow-hidden">
                <!-- Module Header Banner -->
                <div id="module-header-bg" class="p-8 text-white relative">
                    <div class="relative z-10 space-y-2">
                        <span id="module-category-badge" class="bg-white/20 backdrop-blur-md px-3 py-1 rounded-full text-xs font-bold uppercase tracking-wider">
                            Kategori
                        </span>
                        <h1 id="module-title-display" class="text-3xl sm:text-4xl font-bold">Judul Modul Pembelajaran</h1>
                        <p id="module-desc-display" class="text-white/90 text-sm max-w-2xl">Deskripsi modul materi pembelajaran.</p>
                    </div>
                </div>

                <!-- Content Area -->
                <div class="p-6 sm:p-8 space-y-8">
                    <!-- Lesson Material Box -->
                    <div class="bg-slate-50 border-2 border-slate-100 rounded-2xl p-6 space-y-4">
                        <div class="flex items-center space-x-3 text-brand-blue font-fun font-bold text-lg border-b border-slate-200 pb-3">
                            <i class="fa-solid fa-lightbulb text-brand-yellow text-2xl"></i>
                            <span>Rangkuman Materi Seru</span>
                        </div>
                        <div id="module-content-body" class="text-slate-700 leading-relaxed space-y-3 font-medium">
                            <!-- Injected content -->
                        </div>
                    </div>

                    <!-- Quiz Section -->
                    <div class="space-y-6 border-t border-slate-100 pt-6">
                        <div class="flex items-center justify-between">
                            <h2 class="text-2xl font-bold text-slate-800 font-fun">
                                <i class="fa-solid fa-gamepad text-brand-coral mr-2"></i>Kuis Interaktif
                            </h2>
                            <span id="quiz-progress-text" class="text-xs font-bold bg-amber-100 text-amber-800 px-3 py-1 rounded-full">Soal 1 dari 2</span>
                        </div>

                        <!-- Quiz Card -->
                        <div id="quiz-container" class="bg-gradient-to-br from-indigo-50 to-blue-50 border-2 border-indigo-100 rounded-3xl p-6 sm:p-8 space-y-6 shadow-sm">
                            <div class="text-lg sm:text-xl font-bold text-slate-800" id="quiz-question">
                                Pertanyaan kuis akan muncul di sini?
                            </div>

                            <!-- Options Container -->
                            <div id="quiz-options" class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                                <!-- Dynamic Options -->
                            </div>

                            <!-- Quiz Feedback Box -->
                            <div id="quiz-feedback" class="hidden p-4 rounded-2xl font-fun font-bold text-center text-sm transition-all"></div>
                        </div>

                        <!-- Quiz Navigation Buttons -->
                        <div class="flex justify-between items-center">
                            <button id="prev-question-btn" onclick="prevQuestion()" class="px-5 py-2.5 rounded-xl border border-slate-300 font-fun font-bold text-slate-600 hover:bg-slate-100 transition-all text-sm disabled:opacity-50" disabled>
                                <i class="fa-solid fa-chevron-left mr-2"></i>Sebelumnya
                            </button>
                            <button id="next-question-btn" onclick="nextQuestion()" class="px-6 py-2.5 rounded-xl bg-brand-blue text-white font-fun font-bold hover:bg-blue-600 transition-all text-sm shadow-md flex items-center">
                                Selanjutnya <i class="fa-solid fa-chevron-right ml-2"></i>
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- VIEW 3: HALAMAN REKOMENDASI PINTAR & EVALUASI -->
        <section id="view-recommendations" class="hidden space-y-8">
            <div class="bg-white rounded-3xl p-6 sm:p-8 border border-slate-100 shadow-xl space-y-6">
                <div class="flex items-center space-x-4 border-b border-slate-100 pb-6">
                    <div class="w-14 h-14 bg-amber-100 rounded-2xl flex items-center justify-center text-amber-500 text-3xl">
                        <i class="fa-solid fa-brain"></i>
                    </div>
                    <div>
                        <h1 class="text-3xl font-bold text-slate-800">Analisis & Rekomendasi Pintar</h1>
                        <p class="text-slate-500 text-sm">Sistem menganalisis kemampuan anak berdasarkan skor kuis terkini</p>
                    </div>
                </div>

                <!-- Analysis Summary Grid -->
                <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                    <!-- Strength Card -->
                    <div class="bg-emerald-50 border border-emerald-200 rounded-2xl p-5 space-y-2">
                        <div class="flex items-center justify-between text-emerald-700 font-fun font-bold">
                            <span>Kekuatan Utama</span>
                            <i class="fa-solid fa-circle-check text-xl"></i>
                        </div>
                        <div id="user-strength-text" class="text-2xl font-bold text-slate-800">Matematika Dasar</div>
                        <p class="text-xs text-slate-600">Menunjukkan akurasi kuis di atas 85%.</p>
                    </div>

                    <!-- Area to Improve Card -->
                    <div class="bg-amber-50 border border-amber-200 rounded-2xl p-5 space-y-2">
                        <div class="flex items-center justify-between text-amber-700 font-fun font-bold">
                            <span>Perlu Ditingkatkan</span>
                            <i class="fa-solid fa-triangle-exclamation text-xl"></i>
                        </div>
                        <div id="user-weakness-text" class="text-2xl font-bold text-slate-800">Sains & Alam</div>
                        <p class="text-xs text-slate-600">Dapat ditingkatkan dengan kuis interaktif tambahan.</p>
                    </div>

                    <!-- Recommended Learning Style -->
                    <div class="bg-purple-50 border border-purple-200 rounded-2xl p-5 space-y-2">
                        <div class="flex items-center justify-between text-purple-700 font-fun font-bold">
                            <span>Level Rekomendasi</span>
                            <i class="fa-solid fa-layer-group text-xl"></i>
                        </div>
                        <div id="user-recommended-level" class="text-2xl font-bold text-slate-800">Modul Tingkat 2</div>
                        <p class="text-xs text-slate-600">Disesuaikan otomatis oleh algoritma sistem.</p>
                    </div>
                </div>

                <!-- Recommended Path -->
                <div class="space-y-4 pt-4">
                    <h3 class="text-xl font-bold text-slate-800 font-fun">Jalur Belajar yang Disarankan Selanjutnya</h3>
                    <div id="smart-recommendation-list" class="space-y-3">
                        <!-- Dynamic Smart list injected via JS -->
                    </div>
                </div>
            </div>
        </section>

        <!-- VIEW 4: DASHBOARD PENGAJAR / RELAWAN -->
        <section id="view-admin" class="hidden space-y-8">
            <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-4">
                <div>
                    <h1 class="text-3xl font-bold text-slate-800">Portal Pengajar & Relawan</h1>
                    <p class="text-slate-500 text-sm">Monitoring perkembangan anak-anak di Yayasan Tangan Kasih</p>
                </div>
                <button onclick="openAddModuleModal()" class="bg-brand-green text-white font-fun font-bold px-5 py-2.5 rounded-2xl hover:bg-emerald-600 transition-all shadow-md flex items-center justify-center">
                    <i class="fa-solid fa-plus-circle mr-2"></i>Tambah Modul Pembelajaran Baru
                </button>
            </div>

            <!-- Stats Overview Cards -->
            <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6">
                <div class="bg-white p-5 rounded-2xl border border-slate-100 shadow-sm flex items-center space-x-4">
                    <div class="w-12 h-12 bg-blue-100 text-brand-blue rounded-xl flex items-center justify-center text-xl">
                        <i class="fa-solid fa-children"></i>
                    </div>
                    <div>
                        <div class="text-xs font-semibold text-slate-400">Total Anak Aktif</div>
                        <div class="text-2xl font-bold text-slate-800">42 Anak</div>
                    </div>
                </div>

                <div class="bg-white p-5 rounded-2xl border border-slate-100 shadow-sm flex items-center space-x-4">
                    <div class="w-12 h-12 bg-amber-100 text-amber-500 rounded-xl flex items-center justify-center text-xl">
                        <i class="fa-solid fa-star"></i>
                    </div>
                    <div>
                        <div class="text-xs font-semibold text-slate-400">Bintang Diberikan</div>
                        <div class="text-2xl font-bold text-slate-800">3,450 Bintang</div>
                    </div>
                </div>

                <div class="bg-white p-5 rounded-2xl border border-slate-100 shadow-sm flex items-center space-x-4">
                    <div class="w-12 h-12 bg-emerald-100 text-emerald-500 rounded-xl flex items-center justify-center text-xl">
                        <i class="fa-solid fa-circle-check"></i>
                    </div>
                    <div>
                        <div class="text-xs font-semibold text-slate-400">Kuis Selesai</div>
                        <div class="text-2xl font-bold text-slate-800">128 Kuis</div>
                    </div>
                </div>

                <div class="bg-white p-5 rounded-2xl border border-slate-100 shadow-sm flex items-center space-x-4">
                    <div class="w-12 h-12 bg-purple-100 text-brand-purple rounded-xl flex items-center justify-center text-xl">
                        <i class="fa-solid fa-chart-pie"></i>
                    </div>
                    <div>
                        <div class="text-xs font-semibold text-slate-400">Rata-rata Skor</div>
                        <div class="text-2xl font-bold text-slate-800">88.5%</div>
                    </div>
                </div>
            </div>

            <!-- Charts Section -->
            <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
                <!-- Progress Chart -->
                <div class="bg-white p-6 rounded-3xl border border-slate-100 shadow-sm space-y-4">
                    <h3 class="text-lg font-bold text-slate-800 font-fun">Rata-rata Skor per Kategori Materi</h3>
                    <div class="h-64">
                        <canvas id="categoryChart"></canvas>
                    </div>
                </div>

                <!-- Children Progress Table -->
                <div class="bg-white p-6 rounded-3xl border border-slate-100 shadow-sm space-y-4">
                    <h3 class="text-lg font-bold text-slate-800 font-fun">Progres Anak-anak Yayasan</h3>
                    <div class="overflow-x-auto">
                        <table class="w-full text-left border-collapse">
                            <thead>
                                <tr class="border-b border-slate-100 text-xs font-bold text-slate-400 uppercase">
                                    <th class="py-3 px-2">Nama Anak</th>
                                    <th class="py-3 px-2">Modul Selesai</th>
                                    <th class="py-3 px-2">Total Bintang</th>
                                    <th class="py-3 px-2">Status</th>
                                </tr>
                            </thead>
                            <tbody class="text-sm divide-y divide-slate-50 font-medium text-slate-700">
                                <tr>
                                    <td class="py-3 px-2 flex items-center space-x-2">
                                        <img src="https://api.dicebear.com/7.x/bottts/svg?seed=Budi" class="w-6 h-6 rounded-full bg-blue-100">
                                        <span>Budi</span>
                                    </td>
                                    <td class="py-3 px-2">3 Modul</td>
                                    <td class="py-3 px-2 text-amber-600 font-bold">120 <i class="fa-solid fa-star text-xs"></i></td>
                                    <td class="py-3 px-2"><span class="bg-emerald-100 text-emerald-700 text-xs font-bold px-2 py-1 rounded-md">Aktif Belajar</span></td>
                                </tr>
                                <tr>
                                    <td class="py-3 px-2 flex items-center space-x-2">
                                        <img src="https://api.dicebear.com/7.x/bottts/svg?seed=Siti" class="w-6 h-6 rounded-full bg-pink-100">
                                        <span>Siti</span>
                                    </td>
                                    <td class="py-3 px-2">5 Modul</td>
                                    <td class="py-3 px-2 text-amber-600 font-bold">210 <i class="fa-solid fa-star text-xs"></i></td>
                                    <td class="py-3 px-2"><span class="bg-emerald-100 text-emerald-700 text-xs font-bold px-2 py-1 rounded-md">Sangat Aktif</span></td>
                                </tr>
                                <tr>
                                    <td class="py-3 px-2 flex items-center space-x-2">
                                        <img src="https://api.dicebear.com/7.x/bottts/svg?seed=Andi" class="w-6 h-6 rounded-full bg-yellow-100">
                                        <span>Andi</span>
                                    </td>
                                    <td class="py-3 px-2">2 Modul</td>
                                    <td class="py-3 px-2 text-amber-600 font-bold">80 <i class="fa-solid fa-star text-xs"></i></td>
                                    <td class="py-3 px-2"><span class="bg-amber-100 text-amber-700 text-xs font-bold px-2 py-1 rounded-md">Perlu Pendampingan</span></td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </section>

    </main>

    <!-- MODAL: TAMBAH MATERI BARU (ADMIN) -->
    <div id="add-module-modal" class="fixed inset-0 bg-slate-900/40 backdrop-blur-sm z-50 flex items-center justify-center hidden p-4">
        <div class="bg-white rounded-3xl p-6 sm:p-8 max-w-lg w-full space-y-6 shadow-2xl relative">
            <div class="flex justify-between items-center border-b border-slate-100 pb-4">
                <h3 class="text-xl font-bold text-slate-800 font-fun">Tambah Modul Pembelajaran</h3>
                <button onclick="closeAddModuleModal()" class="text-slate-400 hover:text-slate-600 text-xl font-bold">&times;</button>
            </div>

            <form id="add-module-form" onsubmit="handleNewModule(event)" class="space-y-4">
                <div>
                    <label class="block text-xs font-bold text-slate-600 uppercase mb-1">Judul Modul</label>
                    <input type="text" id="new-title" required class="w-full px-4 py-2.5 rounded-xl border border-slate-200 focus:outline-none focus:ring-2 focus:ring-brand-blue text-sm" placeholder="Contoh: Belajar Pecahan Sederhana">
                </div>

                <div class="grid grid-cols-2 gap-4">
                    <div>
                        <label class="block text-xs font-bold text-slate-600 uppercase mb-1">Kategori</label>
                        <select id="new-category" class="w-full px-4 py-2.5 rounded-xl border border-slate-200 focus:outline-none focus:ring-2 focus:ring-brand-blue text-sm">
                            <option value="Matematika">Matematika</option>
                            <option value="Bahasa">Bahasa</option>
                            <option value="Sains">Sains</option>
                            <option value="Karakter">Karakter</option>
                        </select>
                    </div>
                    <div>
                        <label class="block text-xs font-bold text-slate-600 uppercase mb-1">Tingkat / Level</label>
                        <select id="new-level" class="w-full px-4 py-2.5 rounded-xl border border-slate-200 focus:outline-none focus:ring-2 focus:ring-brand-blue text-sm">
                            <option value="Dasar">Dasar</option>
                            <option value="Menengah">Menengah</option>
                            <option value="Lanjutan">Lanjutan</option>
                        </select>
                    </div>
                </div>

                <div>
                    <label class="block text-xs font-bold text-slate-600 uppercase mb-1">Deskripsi Ringkas</label>
                    <textarea id="new-desc" required rows="2" class="w-full px-4 py-2.5 rounded-xl border border-slate-200 focus:outline-none focus:ring-2 focus:ring-brand-blue text-sm" placeholder="Jelaskan ringkas modul ini..."></textarea>
                </div>

                <div class="pt-4 flex justify-end space-x-3">
                    <button type="button" onclick="closeAddModuleModal()" class="px-5 py-2.5 rounded-xl border border-slate-200 font-bold text-slate-600 text-sm hover:bg-slate-50">Batal</button>
                    <button type="submit" class="px-5 py-2.5 rounded-xl bg-brand-green text-white font-bold text-sm hover:bg-emerald-600 shadow-md">Simpan Modul</button>
                </div>
            </form>
        </div>
    </div>

    <!-- FOOTER -->
    <footer class="bg-white border-t border-slate-100 py-6 mt-12">
        <div class="max-w-7xl mx-auto px-4 text-center text-xs text-slate-400 font-medium">
            <p>© 2026 Yayasan Tangan Kasih. Media Pembelajaran Interaktif Berbasis Web & Rekomendasi Pintar.</p>
        </div>
    </footer>

    <script>
        // APP STATE & DATA
        let currentUser = {
            id: 'budi',
            name: 'Budi',
            level: 'Pemula',
            stars: 120,
            scores: {
                'Matematika': 90,
                'Bahasa': 75,
                'Sains': 50,
                'Karakter': 85
            }
        };

        const usersData = {
            'budi': {
                id: 'budi',
                name: 'Budi',
                level: 'Pemula',
                stars: 120,
                scores: { 'Matematika': 90, 'Bahasa': 70, 'Sains': 50, 'Karakter': 85 }
            },
            'siti': {
                id: 'siti',
                name: 'Siti',
                level: 'Menengah',
                stars: 210,
                scores: { 'Matematika': 60, 'Bahasa': 95, 'Sains': 88, 'Karakter': 90 }
            }
        };

        currentUser = usersData['budi'];
        const completedModules = {};

        let modules = [
            {
                id: 'mod-1',
                title: 'Penjumlahan Seru 1-20',
                category: 'Matematika',
                level: 'Dasar',
                color: 'from-blue-400 to-indigo-500',
                icon: 'fa-calculator',
                description: 'Belajar berhitung dan menjumlahkan angka dengan bantuan benda visual!',
                content: '<p>Penjumlahan adalah menggabungkan dua kelompok benda menjadi satu kelompok besar.</p><p class="bg-blue-100 p-3 rounded-xl border border-blue-200">Contoh: 🍎🍎 (2 apel) + 🍎🍎🍎 (3 apel) = 🍎🍎🍎🍎🍎 (5 apel).</p>',
                quizzes: [
                    {
                        question: 'Berapakah hasil dari 5 + 3 ?',
                        options: ['6', '7', '8', '9'],
                        correct: 2
                    },
                    {
                        question: 'Siti punya 4 balon. Budi memberi 4 balon lagi. Berapa total balon Siti?',
                        options: ['8', '7', '6', '10'],
                        correct: 0
                    }
                ]
            },
            {
                id: 'mod-2',
                title: 'Mengenal Hewan & Habitatnya',
                category: 'Sains',
                level: 'Dasar',
                color: 'from-emerald-400 to-teal-600',
                icon: 'fa-frog',
                description: 'Mari menjelajahi dunia hewan dan tempat tinggal mereka di alam!',
                content: '<p>Hewan hidup di berbagai tempat sesuai kebutuhan mereka. Ada yang di darat, air, atau keduanya (amfibi).</p><p class="bg-emerald-100 p-3 rounded-xl border border-emerald-200">Ikan bernapas dengan insang di air, sedangkan Burung terbang di udara dan hinggap di darat.</p>',
                quizzes: [
                    {
                        question: 'Hewan manakah yang hidup di air dan bernapas dengan insang?',
                        options: ['Kucing', 'Ikan', 'Kelinci', 'Burung'],
                        correct: 1
                    },
                    {
                        question: 'Di manakah tempat tinggal utama seekor burung hantu?',
                        options: ['Di dalam air', 'Di laut lepas', 'Di pepohonan / darat', 'Di dalam tanah'],
                        correct: 2
                    }
                ]
            },
            {
                id: 'mod-3',
                title: 'Huruf Vokal & Kata Sederhana',
                category: 'Bahasa',
                level: 'Dasar',
                color: 'from-pink-400 to-rose-500',
                icon: 'fa-font',
                description: 'Mengenal huruf A, I, U, E, O dan merangkai kata pertama kamu.',
                content: '<p>Huruf vokal terdiri dari lima huruf utama: <strong>A - I - U - E - O</strong>.</p><p class="bg-pink-100 p-3 rounded-xl border border-pink-200">Huruf vokal membantu memberikan suara hidup pada setiap kata!</p>',
                quizzes: [
                    {
                        question: 'Huruf manakah di bawah ini yang merupakan huruf vokal?',
                        options: ['B', 'K', 'U', 'M'],
                        correct: 2
                    },
                    {
                        question: 'Kata "A-P-E-L" diawali dengan huruf vokal apa?',
                        options: ['A', 'I', 'U', 'E'],
                        correct: 0
                    }
                ]
            },
            {
                id: 'mod-4',
                title: 'Saling Menyayangi & Berbagi',
                category: 'Karakter',
                level: 'Dasar',
                color: 'from-amber-400 to-orange-500',
                icon: 'fa-hand-holding-heart',
                description: 'Belajar menjadi anak yang baik hati, suka menolong, dan bersyukur.',
                content: '<p>Berbagi dengan teman di yayasan membuat hati kita gembira dan teman bahagia.</p><p class="bg-amber-100 p-3 rounded-xl border border-amber-200">Jangan lupa mengucapkan "Terima Kasih" saat menerima bantuan!</p>',
                quizzes: [
                    {
                        question: 'Apa yang harus kita ucapkan saat teman memberi kita hadiah atau bantuan?',
                        options: ['Maaf', 'Terima Kasih', 'Permisi', 'Tidak Mau'],
                        correct: 1
                    }
                ]
            }
        ];

        let currentActiveModule = null;
        let currentQuizIndex = 0;
        let userAnswers = {};

        // INITIALIZATION
        window.onload = function() {
            renderDashboard();
            renderAdminAnalytics();
        };

        // NAVIGATION LOGIC
        function switchView(viewName) {
            document.getElementById('view-dashboard').classList.add('hidden');
            document.getElementById('view-module').classList.add('hidden');
            document.getElementById('view-recommendations').classList.add('hidden');
            document.getElementById('view-admin').classList.add('hidden');

            // Reset navigation button active states
            document.querySelectorAll('.nav-btn').forEach(btn => {
                btn.classList.remove('bg-white', 'text-brand-blue', 'shadow-sm');
                btn.classList.add('text-slate-600');
            });

            const activeNav = document.getElementById(`nav-${viewName}`);
            if (activeNav) {
                activeNav.classList.add('bg-white', 'text-brand-blue', 'shadow-sm');
                activeNav.classList.remove('text-slate-600');
            }

            if (viewName === 'dashboard') {
                document.getElementById('view-dashboard').classList.remove('hidden');
                renderDashboard();
            } else if (viewName === 'module') {
                document.getElementById('view-module').classList.remove('hidden');
            } else if (viewName === 'recommendations') {
                document.getElementById('view-recommendations').classList.remove('hidden');
                renderSmartRecommendationsPage();
            } else if (viewName === 'admin') {
                document.getElementById('view-admin').classList.remove('hidden');
            }
        }

        function scrollToRecommendations() {
            document.getElementById('recommendation-section').scrollIntoView({ behavior: 'smooth' });
        }

        // USER SWITCHER
        function selectUser(userId) {
            currentUser = usersData[userId];
            document.getElementById('user-name').innerText = currentUser.name;
            document.getElementById('banner-user-name').innerText = currentUser.name;
            document.getElementById('user-level').innerText = `Level - ${currentUser.level}`;
            document.getElementById('user-stars').innerText = currentUser.stars;
            document.getElementById('user-avatar').src = `https://api.dicebear.com/7.x/bottts/svg?seed=${currentUser.name}`;

            renderDashboard();
            renderSmartRecommendationsPage();
        }

        // RECOMMENDATION ALGORITHM
        function getRecommendedModules() {
            // Find category with lowest score for current user
            let lowestCategory = 'Sains';
            let lowestScore = 100;

            for (const [cat, score] of Object.entries(currentUser.scores)) {
                if (score < lowestScore) {
                    lowestScore = score;
                    lowestCategory = cat;
                }
            }

            // Prioritize modules matching lowest score category
            const recommended = modules.filter(m => m.category === lowestCategory);
            const others = modules.filter(m => m.category !== lowestCategory);

            return {
                primary: recommended.length > 0 ? recommended[0] : modules[0],
                secondary: others.slice(0, 2),
                targetCategory: lowestCategory
            };
        }

        // RENDER DASHBOARD
        function renderDashboard() {
            const rec = getRecommendedModules();
            const recContainer = document.getElementById('recommendation-cards-container');

            // Render Recommendation Banner Card
            recContainer.innerHTML = `
                <div class="bg-gradient-to-r from-amber-400 to-orange-400 rounded-3xl p-6 text-white shadow-lg flex flex-col justify-between space-y-4 bouncy-hover">
                    <div class="space-y-2">
                        <div class="flex items-center justify-between">
                            <span class="bg-white/30 text-white font-bold text-xs px-3 py-1 rounded-full uppercase">Rekomendasi Utama</span>
                            <span class="text-xs bg-amber-900/20 px-2 py-1 rounded-md font-semibold">Prioritas Belajar</span>
                        </div>
                        <h3 class="text-2xl font-bold font-fun">${rec.primary.title}</h3>
                        <p class="text-amber-50 text-xs">${rec.primary.description}</p>
                    </div>
                    <div class="flex items-center justify-between pt-2">
                        <div class="text-xs font-bold bg-white/20 px-3 py-1 rounded-lg">
                            <i class="fa-solid fa-bullseye mr-1"></i>Sesuai Evaluasi ${rec.targetCategory}
                        </div>
                        <button onclick="openModule('${rec.primary.id}')" class="bg-white text-orange-600 font-fun font-bold px-4 py-2 rounded-xl shadow-md hover:bg-slate-50 transition-all text-sm">
                            Mulai Belajar <i class="fa-solid fa-play ml-1"></i>
                        </button>
                    </div>
                </div>

                <div class="bg-white border border-slate-100 rounded-3xl p-6 shadow-sm flex flex-col justify-between space-y-4">
                    <div class="space-y-2">
                        <div class="flex items-center justify-between">
                            <span class="bg-blue-100 text-brand-blue font-bold text-xs px-3 py-1 rounded-full uppercase">Materi Penguat</span>
                            <span class="text-xs text-slate-400">Pilihan Kedua</span>
                        </div>
                        <h3 class="text-xl font-bold text-slate-800 font-fun">${rec.secondary[0] ? rec.secondary[0].title : 'Eksplorasi Lain'}</h3>
                        <p class="text-slate-500 text-xs">${rec.secondary[0] ? rec.secondary[0].description : 'Latih kemampuanmu lebih jauh.'}</p>
                    </div>
                    <div class="flex items-center justify-between pt-2">
                        <span class="text-xs text-slate-400 font-medium">+20 Bintang Kuis</span>
                        <button onclick="openModule('${(rec.secondary[0] || rec.primary).id}')" class="bg-slate-100 text-slate-700 font-fun font-bold px-4 py-2 rounded-xl hover:bg-brand-blue hover:text-white transition-all text-sm">
                            Coba Sekarang
                        </button>
                    </div>
                </div>
            `;

            // Render Grid Modules
            renderModulesGrid(modules);
        }

        function renderModulesGrid(moduleList) {
            const grid = document.getElementById('modules-grid');
            grid.innerHTML = '';

            moduleList.forEach(m => {
                const card = document.createElement('div');
                card.className = 'bg-white rounded-3xl border border-slate-100 p-5 shadow-sm hover:shadow-md transition-all flex flex-col justify-between space-y-4 bouncy-hover';
                
                card.innerHTML = `
                    <div class="space-y-3">
                        <div class="w-12 h-12 rounded-2xl bg-gradient-to-tr ${m.color} text-white flex items-center justify-center text-2xl shadow-sm">
                            <i class="fa-solid ${m.icon}"></i>
                        </div>
                        <div>
                            <span class="text-[10px] font-bold uppercase tracking-wider text-slate-400">${m.category} • ${m.level}</span>
                            <h3 class="text-lg font-bold text-slate-800 font-fun leading-tight">${m.title}</h3>
                        </div>
                        <p class="text-slate-500 text-xs line-clamp-2">${m.description}</p>
                    </div>

                    <div class="pt-2 border-t border-slate-50 flex items-center justify-between">
                        <span class="text-xs font-bold text-amber-500"><i class="fa-solid fa-star mr-1"></i>+15 Poin</span>
                        <button onclick="openModule('${m.id}')" class="bg-slate-50 text-brand-blue font-fun font-bold px-3 py-1.5 rounded-xl border border-slate-200 hover:bg-brand-blue hover:text-white transition-all text-xs">
                            Buka Modul
                        </button>
                    </div>
                `;
                grid.appendChild(card);
            });
        }

        function filterModules(category, el) {
            document.querySelectorAll('.filter-btn').forEach(btn => {
                btn.classList.remove('bg-white', 'text-brand-blue', 'shadow-sm');
                btn.classList.add('text-slate-600');
            });
            el.classList.add('bg-white', 'text-brand-blue', 'shadow-sm');
            el.classList.remove('text-slate-600');

            if (category === 'all') {
                renderModulesGrid(modules);
            } else {
                const filtered = modules.filter(m => m.category === category);
                renderModulesGrid(filtered);
            }
        }

        // MODULE PLAYER LOGIC
        function openModule(moduleId) {
            currentActiveModule = modules.find(m => m.id === moduleId);
            if (!currentActiveModule) return;

            currentQuizIndex = 0;
            userAnswers = {};

            // Render Header
            const header = document.getElementById('module-header-bg');
            header.className = `p-8 text-white relative rounded-t-3xl bg-gradient-to-r ${currentActiveModule.color}`;
            document.getElementById('module-category-badge').innerText = `${currentActiveModule.category} • Level ${currentActiveModule.level}`;
            document.getElementById('module-title-display').innerText = currentActiveModule.title;
            document.getElementById('module-desc-display').innerText = currentActiveModule.description;
            document.getElementById('module-content-body').innerHTML = currentActiveModule.content;

            renderQuiz();
            switchView('module');
        }

        function renderQuiz() {
            const quiz = currentActiveModule.quizzes[currentQuizIndex];
            const total = currentActiveModule.quizzes.length;

            document.getElementById('quiz-progress-text').innerText = `Soal ${currentQuizIndex + 1} dari ${total}`;
            document.getElementById('quiz-question').innerText = quiz.question;

            const optionsContainer = document.getElementById('quiz-options');
            optionsContainer.innerHTML = '';

            const feedbackBox = document.getElementById('quiz-feedback');
            feedbackBox.classList.add('hidden');

            quiz.options.forEach((opt, idx) => {
                const btn = document.createElement('button');
                btn.className = `option-btn w-full text-left p-4 rounded-2xl border-2 font-semibold text-slate-700 transition-all flex items-center justify-between ${userAnswers[currentQuizIndex] === idx ? 'border-brand-blue bg-blue-50' : 'border-slate-200 bg-white hover:border-slate-300'}`;
                
                btn.innerHTML = `
                    <span>${opt}</span>
                    <i class="fa-regular fa-circle text-slate-300"></i>
                `;
                btn.onclick = () => selectOption(idx);
                optionsContainer.appendChild(btn);
            });

            // Update Navigation state
            if (userAnswers[currentQuizIndex] !== undefined) applyAnswer(userAnswers[currentQuizIndex], false);

            document.getElementById('prev-question-btn').disabled = currentQuizIndex === 0;
            document.getElementById('next-question-btn').innerText = (currentQuizIndex === total - 1) ? 'Selesaikan Kuis 🎉' : 'Selanjutnya';
        }

        function selectOption(optionIndex) {
            if (userAnswers[currentQuizIndex] !== undefined) return; // jawaban terkunci
            userAnswers[currentQuizIndex] = optionIndex;
            applyAnswer(optionIndex, true);
        }

        function applyAnswer(optionIndex, withSound) {
            const quiz = currentActiveModule.quizzes[currentQuizIndex];
            const feedbackBox = document.getElementById('quiz-feedback');
            if (optionIndex === quiz.correct) {
                if (withSound) playAudioTone(587.33, 'sine');
                feedbackBox.className = 'p-4 rounded-2xl font-fun font-bold text-center text-sm bg-emerald-100 text-emerald-800 border border-emerald-200 block';
                feedbackBox.innerHTML = '<i class="fa-solid fa-circle-check mr-2"></i>Hebat! Jawabanmu Tepat Sekali ⭐';
            } else {
                if (withSound) playAudioTone(220, 'sawtooth');
                feedbackBox.className = 'p-4 rounded-2xl font-fun font-bold text-center text-sm bg-rose-100 text-rose-800 border border-rose-200 block';
                feedbackBox.innerHTML = '<i class="fa-solid fa-circle-xmark mr-2"></i>Hampir Benar, Jawaban yang tepat ditandai hijau ya!';
            }
            renderQuizOptionsHighlight(optionIndex, quiz.correct);
        }

        function renderQuizOptionsHighlight(selected, correct) {
            const btns = document.querySelectorAll('.option-btn');
            btns.forEach((btn, idx) => {
                if (idx === correct) {
                    btn.className = 'option-btn w-full text-left p-4 rounded-2xl border-2 font-semibold transition-all flex items-center justify-between border-emerald-500 bg-emerald-50 text-emerald-800';
                } else if (idx === selected && selected !== correct) {
                    btn.className = 'option-btn w-full text-left p-4 rounded-2xl border-2 font-semibold transition-all flex items-center justify-between border-rose-400 bg-rose-50 text-rose-800';
                } else {
                    btn.className = 'option-btn w-full text-left p-4 rounded-2xl border-2 font-semibold text-slate-400 bg-white opacity-60';
                }
            });
        }

        function nextQuestion() {
            if (userAnswers[currentQuizIndex] === undefined) {
                const fb = document.getElementById('quiz-feedback');
                fb.className = 'p-4 rounded-2xl font-fun font-bold text-center text-sm bg-amber-100 text-amber-800 border border-amber-200 block';
                fb.innerHTML = 'Pilih satu jawaban dulu ya 😊';
                return;
            }
            const total = currentActiveModule.quizzes.length;
            if (currentQuizIndex < total - 1) {
                currentQuizIndex++;
                renderQuiz();
            } else {
                finishQuiz();
            }
        }

        function prevQuestion() {
            if (currentQuizIndex > 0) {
                currentQuizIndex--;
                renderQuiz();
            }
        }

        function finishQuiz() {
            // Calculate Score
            let correctCount = 0;
            currentActiveModule.quizzes.forEach((q, idx) => {
                if (userAnswers[idx] === q.correct) correctCount++;
            });

            const scorePercent = Math.round((correctCount / currentActiveModule.quizzes.length) * 100);
            
            // Update User Profile Stars & Scores
            const doneKey = currentUser.id + ':' + currentActiveModule.id;
            const firstTime = !completedModules[doneKey];
            completedModules[doneKey] = true;
            if (firstTime) currentUser.stars += 20;
            currentUser.scores[currentActiveModule.category] = Math.max(currentUser.scores[currentActiveModule.category], scorePercent);
            
            document.getElementById('user-stars').innerText = currentUser.stars;

            alert(`Selamat! Kamu menyelesaikan Kuis ${currentActiveModule.title}.\nSkor Kamu: ${scorePercent}%\n${firstTime ? 'Kamu mendapatkan +20 Bintang! ⭐' : 'Modul ini sudah pernah diselesaikan, bintang tidak bertambah.'}`);
            switchView('recommendations');
        }

        // AUDIO EFFECTS SYNTHESIZER
        function playAudioTone(freq, type) {
            try {
                const ctx = new (window.AudioContext || window.webkitAudioContext)();
                const osc = ctx.createOscillator();
                const gain = ctx.createGain();
                osc.type = type;
                osc.frequency.value = freq;
                osc.connect(gain);
                gain.connect(ctx.destination);
                osc.start();
                gain.gain.setValueAtTime(0.2, ctx.currentTime);
                gain.gain.exponentialRampToValueAtTime(0.00001, ctx.currentTime + 0.3);
                osc.stop(ctx.currentTime + 0.35);
            } catch(e) {
                // Audio Context fallback silent
            }
        }

        // SMART RECOMMENDATION ANALYTICS PAGE
        function renderSmartRecommendationsPage() {
            // Find Strongest & Weakest Category
            let bestCat = 'Matematika';
            let worstCat = 'Sains';
            let maxScore = -1;
            let minScore = 101;

            for (const [cat, score] of Object.entries(currentUser.scores)) {
                if (score > maxScore) {
                    maxScore = score;
                    bestCat = cat;
                }
                if (score < minScore) {
                    minScore = score;
                    worstCat = cat;
                }
            }

            document.getElementById('user-strength-text').innerText = `${bestCat} (${maxScore}%)`;
            document.getElementById('user-weakness-text').innerText = `${worstCat} (${minScore}%)`;
            document.getElementById('user-recommended-level').innerText = minScore < 60 ? 'Tingkat Dasar' : 'Tingkat Menengah';

            // Recommended Items List
            const listContainer = document.getElementById('smart-recommendation-list');
            const rec = getRecommendedModules();

            listContainer.innerHTML = `
                <div class="p-4 rounded-2xl border-2 border-brand-yellow/50 bg-amber-50/50 flex items-center justify-between">
                    <div class="flex items-center space-x-3">
                        <div class="w-10 h-10 rounded-xl bg-amber-400 text-white flex items-center justify-center font-bold">1</div>
                        <div>
                            <div class="font-bold text-slate-800">${rec.primary.title}</div>
                            <div class="text-xs text-slate-500">Materi ${rec.primary.category} untuk meningkatkan pemahaman area fokus.</div>
                        </div>
                    </div>
                    <button onclick="openModule('${rec.primary.id}')" class="px-4 py-2 bg-brand-yellow text-slate-900 font-bold font-fun rounded-xl text-xs hover:bg-amber-300">
                        Mulai Modul Ini
                    </button>
                </div>
            `;
        }

        // ADMIN / VOLUNTEER FUNCTIONS
        function openAddModuleModal() {
            document.getElementById('add-module-modal').classList.remove('hidden');
        }

        function closeAddModuleModal() {
            document.getElementById('add-module-modal').classList.add('hidden');
        }

        function handleNewModule(e) {
            e.preventDefault();
            const title = document.getElementById('new-title').value;
            const category = document.getElementById('new-category').value;
            const level = document.getElementById('new-level').value;
            const desc = document.getElementById('new-desc').value;

            const newMod = {
                id: 'mod-' + (modules.length + 1),
                title: title,
                category: category,
                level: level,
                color: 'from-purple-400 to-indigo-500',
                icon: 'fa-book-bookmark',
                description: desc,
                content: `<p>${desc}</p>`,
                quizzes: [
                    {
                        question: `Soal Latihan Dasar untuk modul ${title}?`,
                        options: ['Jawaban A', 'Jawaban B (Benar)', 'Jawaban C', 'Jawaban D'],
                        correct: 1
                    }
                ]
            };

            modules.push(newMod);
            closeAddModuleModal();
            alert('Modul baru berhasil ditambahkan oleh Relawan!');
            renderDashboard();
        }

        // RENDER ADMIN CHART
        function renderAdminAnalytics() {
            const ctx = document.getElementById('categoryChart').getContext('2d');
            new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: ['Matematika', 'Bahasa', 'Sains', 'Karakter'],
                    datasets: [{
                        label: 'Rata-Rata Skor Anak (%)',
                        data: [85, 78, 62, 90],
                        backgroundColor: [
                            '#4A90E2',
                            '#FF6B6B',
                            '#06D6A0',
                            '#FFD166'
                        ],
                        borderRadius: 10
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: { display: false }
                    },
                    scales: {
                        y: { beginAtZero: true, max: 100 }
                    }
                }
            });
        }
    </script>
</body>
</html>
