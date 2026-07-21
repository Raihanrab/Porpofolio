<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Portofolio | Editor Video & Foto</title>
    <style>
        /* CSS Variables untuk Skema Warna */
        :root {
            --bg-color: #121212;
            --surface-color: #1e1e1e;
            --text-primary: #ffffff;
            --text-secondary: #a0a0a0;
            --accent-color: #00adb5; /* Aksen modern cyan/teal */
            --border-color: #333333;
        }

        /* Reset & Base Styles */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
        }

        html {
            scroll-behavior: smooth;
            scroll-padding-top: 80px; /* Offset untuk fixed navbar */
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-primary);
            line-height: 1.6;
        }

        a {
            text-decoration: none;
            color: inherit;
        }

        /* Typography */
        h1, h2, h3, h4 { color: var(--text-primary); }
        h2 {
            font-size: 2.5rem;
            margin-bottom: 2rem;
            display: inline-block;
            border-bottom: 3px solid var(--accent-color);
            padding-bottom: 0.5rem;
        }
        p { color: var(--text-secondary); margin-bottom: 1rem; }

        /* Navbar */
        nav {
            position: fixed;
            top: 0;
            width: 100%;
            background-color: rgba(18, 18, 18, 0.9);
            backdrop-filter: blur(10px);
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 1.5rem 5%;
            z-index: 1000;
            border-bottom: 1px solid var(--border-color);
        }

        .logo { font-size: 1.5rem; font-weight: bold; letter-spacing: 1px; color: var(--text-primary);}
        .logo span { color: var(--accent-color); }

        .nav-links { display: flex; gap: 1.5rem; list-style: none; }
        .nav-links li a {
            font-size: 0.95rem;
            font-weight: 500;
            transition: color 0.3s ease;
        }
        .nav-links li a:hover { color: var(--accent-color); }

        /* Layout Container */
        .container { max-width: 1200px; margin: 0 auto; padding: 4rem 5%; }
        section { min-height: 80vh; padding: 4rem 0; }

        /* Hero / Biodata Section */
        #biodata {
            display: flex;
            align-items: center;
            justify-content: space-between;
            min-height: 100vh;
            padding-top: 8rem;
        }

        .hero-content { flex: 1; padding-right: 2rem; }
        .hero-content h3 { font-size: 1.5rem; color: var(--accent-color); font-weight: 400; margin-bottom: 0.5rem; }
        .hero-content h1 { font-size: 3.5rem; margin-bottom: 1rem; line-height: 1.2; }
        .hero-content p { font-size: 1.1rem; margin-bottom: 2rem; max-width: 600px; }
        
        .hero-image {
            flex: 1;
            display: flex;
            justify-content: center;
        }
        .hero-image img {
            width: 350px;
            height: 350px;
            border-radius: 50%;
            object-fit: cover;
            border: 4px solid var(--surface-color);
            box-shadow: 0 0 20px rgba(0, 173, 181, 0.2);
        }

        /* Buttons */
        .btn {
            display: inline-block;
            padding: 0.8rem 1.8rem;
            border-radius: 5px;
            font-weight: 600;
            transition: all 0.3s ease;
            cursor: pointer;
            margin-right: 1rem;
        }
        .btn-primary { background-color: var(--accent-color); color: #121212; border: 2px solid var(--accent-color); }
        .btn-primary:hover { background-color: transparent; color: var(--accent-color); }
        .btn-outline { background-color: transparent; border: 2px solid var(--text-secondary); color: var(--text-primary); }
        .btn-outline:hover { border-color: var(--accent-color); color: var(--accent-color); }

        /* Grid Layout for Cards */
        .grid-container {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
            gap: 2rem;
        }

        /* Cards (Portfolio, Pengalaman, dll) */
        .card {
            background-color: var(--surface-color);
            border-radius: 10px;
            padding: 1.5rem;
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            border: 1px solid var(--border-color);
        }
        .card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(0,0,0,0.3);
            border-color: var(--accent-color);
        }

        /* Portfolio Specific */
        .portfolio-img {
            width: 100%;
            height: 200px;
            background-color: #333;
            border-radius: 5px;
            margin-bottom: 1rem;
            object-fit: cover;
        }
        .card h4 { font-size: 1.2rem; margin-bottom: 0.5rem; }
        .role-tag { display: inline-block; font-size: 0.8rem; background: rgba(0, 173, 181, 0.1); color: var(--accent-color); padding: 0.2rem 0.6rem; border-radius: 3px; margin-bottom: 1rem; }

        /* Skills */
        .skills-container { display: flex; flex-wrap: wrap; gap: 1rem; }
        .skill-badge {
            background-color: var(--surface-color);
            padding: 0.8rem 1.5rem;
            border-radius: 30px;
            font-size: 1rem;
            border: 1px solid var(--border-color);
            transition: 0.3s;
        }
        .skill-badge:hover { border-color: var(--accent-color); color: var(--accent-color); }

        /* Timeline (Pengalaman & Pendidikan) */
        .timeline-item { margin-bottom: 2rem; padding-left: 1.5rem; border-left: 2px solid var(--border-color); position: relative; }
        .timeline-item::before {
            content: ''; position: absolute; left: -6px; top: 5px;
            width: 10px; height: 10px; border-radius: 50%;
            background-color: var(--accent-color);
        }
        .timeline-date { font-size: 0.9rem; color: var(--accent-color); margin-bottom: 0.5rem; font-weight: 600; }

        /* Contact Section */
        .contact-info { display: flex; flex-direction: column; gap: 1rem; }
        .contact-item { display: flex; align-items: center; gap: 1rem; font-size: 1.1rem; }

        /* Footer */
        footer { text-align: center; padding: 2rem; background-color: var(--surface-color); color: var(--text-secondary); border-top: 1px solid var(--border-color); }

        /* Responsive Design */
        @media (max-width: 900px) {
            #biodata { flex-direction: column-reverse; text-align: center; padding-top: 6rem; }
            .hero-content { padding-right: 0; margin-top: 2rem; }
            .hero-content p { margin: 0 auto 2rem; }
            .nav-links { display: none; /* Hide on mobile for simplicity in this demo */ }
        }
    </style>
</head>
<body>

    <!-- 1. Header / Navbar -->
    <nav>
        <div class="logo">[Nama]<span>.</span></div>
        <ul class="nav-links">
            <li><a href="#biodata">Biodata</a></li>
            <li><a href="#portfolio">Portfolio</a></li>
            <li><a href="#keahlian">Keahlian</a></li>
            <li><a href="#pengalaman-kerja">Kerja</a></li>
            <li><a href="#pengalaman-organisasi">Organisasi</a></li>
            <li><a href="#pendidikan">Pendidikan</a></li>
            <li><a href="#sertifikat">Sertifikat</a></li>
            <li><a href="#kontak">Kontak</a></li>
        </ul>
    </nav>

    <!-- 2. Hero + Biodata -->
    <section id="biodata">
        <div class="container" style="display: flex; align-items: center; justify-content: space-between; flex-wrap: wrap;">
            <div class="hero-content">
                <h3>Halo, perkenalkan saya</h3>
                <h1>[Nama Lengkap Anda]</h1>
                <p>Saya seorang <strong>Video & Photo Editor</strong> yang berdomisili di [Kota Anda]. Saya memiliki ketertarikan besar dalam merangkai visual yang menarik, cinematic color grading, dan penceritaan melalui medium digital. Siap membantu menghidupkan ide Anda menjadi karya visual yang luar biasa.</p>
                <a href="#portfolio" class="btn btn-primary">Lihat Portfolio</a>
                <a href="#kontak" class="btn btn-outline">Hubungi Saya</a>
            </div>
            <div class="hero-image">
                <!-- Ganti src dengan URL foto Anda -->
                <img src="https://via.placeholder.com/350" alt="Foto Profil [Nama Anda]">
            </div>
        </div>
    </section>

    <!-- 3. Portfolio -->
    <section id="portfolio" class="container">
        <h2>Portfolio</h2>
        <div class="grid-container">
            <!-- Card 1 -->
            <a href="#" class="card">
                <img src="https://via.placeholder.com/400x200" alt="Thumbnail Project" class="portfolio-img">
                <h4>[Judul Proyek Video 1]</h4>
                <span class="role-tag">Video Editor & Colorist</span>
                <p>Deskripsi singkat mengenai proyek ini. Menggunakan transisi dinamis dan color grading cinematic untuk video komersial.</p>
            </a>
            <!-- Card 2 -->
            <a href="#" class="card">
                <img src="https://via.placeholder.com/400x200" alt="Thumbnail Project" class="portfolio-img">
                <h4>[Judul Proyek Foto 1]</h4>
                <span class="role-tag">Retoucher / Photo Editor</span>
                <p>Proses retouching foto produk kecantikan untuk kebutuhan sosial media dan billboard digital.</p>
            </a>
            <!-- Card 3 -->
            <a href="#" class="card">
                <img src="https://via.placeholder.com/400x200" alt="Thumbnail Project" class="portfolio-img">
                <h4>[Judul Proyek Video 2]</h4>
                <span class="role-tag">Motion Graphic & Editor</span>
                <p>Pembuatan video promosi event menggunakan perpaduan footage dan elemen motion graphics.</p>
            </a>
        </div>
    </section>

    <!-- 4. Keahlian -->
    <section id="keahlian" class="container">
        <h2>Keahlian & Tools</h2>
        <div class="skills-container">
            <span class="skill-badge">Video Editing</span>
            <span class="skill-badge">Photo Retouching</span>
            <span class="skill-badge">Color Grading</span>
            <span class="skill-badge">Basic Motion Graphic</span>
            <span class="skill-badge">Adobe Premiere Pro</span>
            <span class="skill-badge">Adobe After Effects</span>
            <span class="skill-badge">Adobe Photoshop</span>
            <span class="skill-badge">Adobe Lightroom</span>
            <span class="skill-badge">DaVinci Resolve</span>
        </div>
    </section>

    <!-- 5. Pengalaman Kerja -->
    <section id="pengalaman-kerja" class="container">
        <h2>Pengalaman Kerja</h2>
        <div class="timeline-item">
            <div class="timeline-date">Jan 2022 - Sekarang</div>
            <h4>Senior Video Editor - [Nama Perusahaan/Agency]</h4>
            <p><strong>Tugas Utama:</strong> Bertanggung jawab penuh atas pasca-produksi konten video YouTube dan Instagram Reels klien. <br>
            <strong>Pencapaian:</strong> Meningkatkan retensi penonton hingga 40% melalui gaya editing yang dinamis.</p>
        </div>
        <div class="timeline-item">
            <div class="timeline-date">Mar 2020 - Des 2021</div>
            <h4>Freelance Photo Editor - [Nama Platform/Klien]</h4>
            <p><strong>Tugas Utama:</strong> Melakukan color correction dan batch editing foto pernikahan dan event. <br>
            <strong>Pencapaian:</strong> Menyelesaikan lebih dari 50+ proyek tepat waktu dengan rating kepuasan 5/5.</p>
        </div>
    </section>

    <!-- 6. Pengalaman Organisasi -->
    <section id="pengalaman-organisasi" class="container">
        <h2>Pengalaman Organisasi</h2>
        <div class="timeline-item">
            <div class="timeline-date">2019 - 2020</div>
            <h4>Ketua Divisi Media & Publikasi - [Nama Organisasi/Kampus]</h4>
            <p><strong>Tanggung Jawab:</strong> Mengelola seluruh aset visual (foto & video) untuk kegiatan organisasi.<br>
            <strong>Kontribusi:</strong> Memproduksi 10+ after movie acara tahunan yang digunakan untuk arsip dan promosi kampus.</p>
        </div>
    </section>

    <!-- 7. Pendidikan -->
    <section id="pendidikan" class="container">
        <h2>Pendidikan</h2>
        <div class="timeline-item">
            <div class="timeline-date">Lulus Tahun 2022</div>
            <h4>[Nama Universitas / Perguruan Tinggi]</h4>
            <p>S1 [Nama Jurusan, misal: Ilmu Komunikasi / Desain Komunikasi Visual]</p>
        </div>
    </section>

    <!-- 8. Sertifikat / Prestasi -->
    <section id="sertifikat" class="container">
        <h2>Sertifikat & Prestasi</h2>
        <div class="grid-container">
            <div class="card">
                <h4>Sertifikasi Adobe Certified Professional</h4>
                <p>Visual Design using Adobe Photoshop (Tahun 2023)</p>
            </div>
            <div class="card">
                <h4>Juara 1 Lomba Video Dokumenter Pendek</h4>
                <p>Tingkat Nasional - Diselenggarakan oleh [Nama Instansi] (Tahun 2021)</p>
            </div>
        </div>
    </section>

    <!-- 9. Kontak -->
    <section id="kontak" class="container">
        <h2>Mari Berkolaborasi!</h2>
        <p>Apakah Anda memiliki proyek menarik? Jangan ragu untuk menghubungi saya melalui kontak di bawah ini.</p>
        <br>
        <div class="contact-info">
            <div class="contact-item">
                📧 <strong>Email:</strong> <a href="mailto:emailanda@gmail.com">emailanda@gmail.com</a>
            </div>
            <div class="contact-item">
                📱 <strong>WhatsApp:</strong> <a href="https://wa.me/6281234567890">+62 812-3456-7890</a>
            </div>
            <div class="contact-item">
                🌐 <strong>Instagram:</strong> <a href="#">@username_anda</a>
            </div>
            <div class="contact-item">
                💼 <strong>LinkedIn:</strong> <a href="#">linkedin.com/in/namaanda</a>
            </div>
        </div>
    </section>

    <!-- Footer -->
    <footer>
        <p>&copy; 2024 [Nama Anda]. Dibuat dengan dedikasi dan kreativitas.</p>
    </footer>

</body>
</html>
