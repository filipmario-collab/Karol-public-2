<!DOCTYPE html>
<html lang="de">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>G&L Stickerei Wien</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;1,400&family=Lato:wght@300;400;700&display=swap" rel="stylesheet">
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.9.4/leaflet.min.css"/>
<style>
  :root {
    --navy: #1a2456;
    --blue: #2e5bba;
    --light-blue: #5b8dd9;
    --gold: #c9a84c;
    --cream: #f9f6f0;
    --white: #ffffff;
  }
  * { margin: 0; padding: 0; box-sizing: border-box; }
  body { font-family: 'Lato', sans-serif; background: var(--white); color: var(--navy); overflow-x: hidden; }
  html { scroll-behavior: smooth; scroll-padding-top: 80px; }

  nav {
    position: fixed; top: 0; left: 0; right: 0; z-index: 1000;
    display: flex; justify-content: space-between; align-items: center;
    padding: 1rem 2rem;
    background: rgba(26,36,86,0.95); backdrop-filter: blur(10px);
    transition: all 0.3s;
  }
  .nav-logo { font-family: 'Playfair Display', serif; font-size: 1.5rem; color: var(--white); font-weight: 700; text-decoration: none; }
  .nav-logo span { color: var(--gold); }
  .menu-toggle { display: none; color: white; font-size: 1.5rem; cursor: pointer; }
  .nav-links { display: flex; gap: 2rem; list-style: none; }
  .nav-links a { color: rgba(255,255,255,0.8); text-decoration: none; font-size: 0.85rem; letter-spacing: 0.1em; text-transform: uppercase; font-weight: 700; transition: 0.2s; }
  .nav-links a:hover { color: var(--gold); }

  @media (max-width: 768px) {
    .menu-toggle { display: block; }
    .nav-links { display: none; position: absolute; top: 100%; left: 0; right: 0; background: var(--navy); flex-direction: column; padding: 2rem; text-align: center; gap: 1.5rem; }
    .nav-links.active { display: flex; }
  }

  .hero {
    min-height: 100vh;
    background: linear-gradient(135deg, var(--navy) 0%, var(--blue) 60%, var(--light-blue) 100%);
    display: flex; flex-direction: column; align-items: center; justify-content: center;
    padding: 2rem; text-align: center;
  }
  .logo-gl { font-family: 'Playfair Display', serif; font-size: clamp(4rem,15vw,8rem); color: var(--white); line-height: 1; position: relative; }
  .logo-gl span { color: var(--gold); }
  .butterfly { font-size: 2.5rem; position: absolute; top: -0.6em; right: -0.5em; animation: flutter 3s infinite; }
  .logo-sub { font-weight: 700; letter-spacing: 0.4em; font-size: clamp(1rem,4vw,1.5rem); color: rgba(255,255,255,0.85); text-transform: uppercase; margin-top: 0.5rem; }
  .hero-tagline { color: rgba(255,255,255,0.6); font-weight: 300; letter-spacing: 0.15em; font-size: 0.95rem; margin-top: 1rem; text-transform: uppercase; }
  .hero-cta { margin-top: 3rem; display: flex; gap: 1rem; flex-wrap: wrap; justify-content: center; }
  .btn { padding: 0.9rem 2rem; border-radius: 2px; font-weight: 700; text-transform: uppercase; font-size: 0.85rem; cursor: pointer; text-decoration: none; transition: 0.3s; }
  .btn-primary { background: var(--gold); color: var(--navy); border: 2px solid var(--gold); }
  .btn-outline { background: transparent; color: var(--white); border: 2px solid rgba(255,255,255,0.4); }

  .section { padding: 6rem 2rem; max-width: 1000px; margin: 0 auto; }
  .section-label { font-size: 0.75rem; letter-spacing: 0.4em; text-transform: uppercase; color: var(--blue); font-weight: 700; margin-bottom: 1rem; }
  .section-title { font-family: 'Playfair Display', serif; font-size: clamp(2rem,5vw,3.5rem); color: #2a3a7a; line-height: 1.2; margin-bottom: 1.5rem; }
  .divider { width: 60px; height: 3px; background: var(--gold); margin: 1.5rem 0; }
  .section-text { font-size: 1.05rem; line-height: 1.8; color: var(--navy); }

  .services-bg { background: var(--navy); padding: 6rem 2rem; color: white; }
  .services-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(220px,1fr)); gap: 2rem; margin-top: 3rem; }
  .service-card { background: rgba(255,255,255,0.05); border: 1px solid rgba(255,255,255,0.1); padding: 2rem; border-radius: 2px; }
  .service-icon { font-size: 2.5rem; margin-bottom: 1rem; }
  .service-title { font-family: 'Playfair Display', serif; font-size: 1.3rem; margin-bottom: 0.5rem; color: var(--white); }

  .gallery-section { background: var(--cream); padding: 6rem 2rem; }
  .gallery-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 1.5rem; margin-top: 3rem; }
  .gallery-item { height: 300px; border-radius: 2px; overflow: hidden; position: relative; }
  .gallery-item img { width: 100%; height: 100%; object-fit: cover; display: block; transition: transform 0.3s; }
  .gallery-item:hover img { transform: scale(1.05); }
  .gallery-label { position: absolute; bottom: 0; left: 0; right: 0; background: rgba(26,36,86,0.7); color: white; font-weight: 700; text-transform: uppercase; letter-spacing: 0.2em; font-size: 0.7rem; padding: 0.5rem; text-align: center; }

  .contact-bg { background: linear-gradient(135deg, var(--blue) 0%, var(--navy) 100%); padding: 6rem 2rem; color: white; }
  .contact-inner { max-width: 1000px; margin: 0 auto; display: grid; grid-template-columns: 1fr 1fr; gap: 4rem; }
  @media (max-width: 768px) { .contact-inner { grid-template-columns: 1fr; } }
  .contact-item { display: flex; align-items: center; gap: 1rem; margin-bottom: 1.2rem; }
  .contact-item a { color: white; text-decoration: none; }
  .contact-icon { width: 44px; height: 44px; background: rgba(255,255,255,0.1); border-radius: 50%; display: flex; align-items: center; justify-content: center; border: 1px solid rgba(255,255,255,0.2); }

  .contact-form-wrap { background: rgba(255,255,255,0.06); padding: 2.5rem; border: 1px solid rgba(255,255,255,0.12); }
  .form-group { margin-bottom: 1.2rem; }
  .form-group label { display: block; font-size: 0.75rem; text-transform: uppercase; margin-bottom: 0.4rem; opacity: 0.6; font-weight: 700; }
  .form-group input, .form-group textarea { width: 100%; padding: 0.8rem; background: rgba(255,255,255,0.07); border: 1px solid rgba(255,255,255,0.15); color: white; border-radius: 2px; outline: none; }
  .form-submit { width: 100%; padding: 1rem; background: var(--gold); border: none; font-weight: 700; text-transform: uppercase; cursor: pointer; transition: 0.3s; color: var(--navy); }

  .map-wrap { max-width: 1000px; margin: 4rem auto 0; height: 350px; border-radius: 2px; overflow: hidden; }
  #map { width: 100%; height: 100%; }

  footer { background: #0f1730; padding: 2rem; text-align: center; color: rgba(255,255,255,0.3); font-size: 0.8rem; }
  @keyframes flutter { 0%,100% { transform:rotate(-5deg) translateY(0); } 50% { transform:rotate(5deg) translateY(-8px); } }
  .reveal { transition: 0.8s all ease-out; }
</style>
</head>
<body>

<nav id="navbar">
  <a href="#" class="nav-logo">G<span>&</span>L</a>
  <div class="menu-toggle" id="mobile-menu">☰</div>
  <ul class="nav-links" id="nav-list">
    <li><a href="#ueber-uns">Über uns</a></li>
    <li><a href="#leistungen">Leistungen</a></li>
    <li><a href="#galerie">Galerie</a></li>
    <li><a href="#kontakt">Kontakt</a></li>
  </ul>
</nav>

<section class="hero">
  <div class="logo-wrap">
    <div class="logo-gl">G<span>&</span>L<span class="butterfly">🦋</span></div>
    <div class="logo-sub">Stickerei</div>
    <div class="hero-tagline">Qualität · Präzision · Wien</div>
  </div>
  <div class="hero-cta">
    <a href="#kontakt" class="btn btn-primary">Anfrage senden</a>
    <a href="#ueber-uns" class="btn btn-outline">Über uns</a>
  </div>
</section>

<section class="section" id="ueber-uns">
  <div class="section-label">Tradition & Moderne</div>
  <h2 class="section-title">Stickerei mit Leidenschaft</h2>
  <div class="divider"></div>
  <p class="section-text">G&L Stickerei steht für hochwertige Stickarbeiten in Wien. Ob individuelle Logos, Vereinskleidung alebo personalisierte Geschenke – wir setzen Ihre Ideen mit höchster Präzision um.</p>
</section>

<section class="services-bg" id="leistungen">
  <div class="section" style="padding:0;">
    <div class="section-label" style="color:var(--gold);">Expertise</div>
    <h2 class="section-title" style="color:white;">Unsere Leistungen</h2>
    <div class="services-grid">
      <div class="service-card"><div class="service-icon">🧵</div><div class="service-title">Logo-Stickerei</div></div>
      <div class="service-card"><div class="service-icon">👕</div><div class="service-title">Vereinsbekleidung</div></div>
      <div class="service-card"><div class="service-icon">🎁</div><div class="service-title">Geschenke</div></div>
      <div class="service-card"><div class="service-icon">🏢</div><div class="service-title">Corporate Wear</div></div>
    </div>
  </div>
</section>

<section class="gallery-section" id="galerie">
  <div class="section" style="padding:0;">
    <div class="section-label">Portfolio</div>
    <h2 class="section-title">Unsere Arbeiten</h2>
    <div class="gallery-grid">
      <div class="gallery-item"><img src="https://raw.githubusercontent.com/filipmario-collab/stickerei-wien/main/logo-polo.jpeg" alt="Logo-Stickerei"><div class="gallery-label">Logo-Stickerei</div></div>
      <div class="gallery-item"><img src="https://raw.githubusercontent.com/filipmario-collab/stickerei-wien/main/logo-blazer.jpeg" alt="Logo-Blazer"><div class="gallery-label">Logo-Stickerei</div></div>
      <div class="gallery-item"><img src="https://raw.githubusercontent.com/filipmario-collab/stickerei-wien/main/team-hoodie.jpeg" alt="Team Hoodie"><div class="gallery-label">Vereinsbekleidung</div></div>
      <div class="gallery-item"><img src="https://raw.githubusercontent.com/filipmario-collab/stickerei-wien/main/team-polo.jpeg" alt="Team Polo"><div class="gallery-label">Vereinsbekleidung</div></div>
      <div class="gallery-item"><img src="https://raw.githubusercontent.com/filipmario-collab/stickerei-wien/main/gift-tote.jpeg" alt="Geschenk Tasche"><div class="gallery-label">Geschenke</div></div>
      <div class="gallery-item"><img src="https://raw.githubusercontent.com/filipmario-collab/stickerei-wien/main/gift-pillow.jpeg" alt="Geschenk Kissen"><div class="gallery-label">Geschenke</div></div>
      <div class="gallery-item"><img src="https://raw.githubusercontent.com/filipmario-collab/stickerei-wien/main/kreation-hoop.jpeg" alt="Kreation"><div class="gallery-label">Spezialarbeiten</div></div>
      <div class="gallery-item"><img src="https://raw.githubusercontent.com/filipmario-collab/stickerei-wien/main/kreation-patches.jpeg" alt="Patches"><div class="gallery-label">Spezialarbeiten</div></div>
    </div>
  </div>
</section>

<section class="contact-bg" id="kontakt">
  <div class="contact-inner">
    <div>
      <div class="section-label" style="color:var(--gold);">Kontakt</div>
      <h2 class="section-title" style="color:white;">Starten Sie Ihr Projekt</h2>
      <div class="contact-item">
        <div class="contact-icon">📞</div>
        <div><a href="tel:+436603512557">+43 660 3512557</a><br><a href="tel:+436602774901">+43 660 2774901</a></div>
      </div>
      <div class="contact-item"><div class="contact-icon">💬</div><a href="https://wa.me/436603512557" target="_blank">WhatsApp Nachricht</a></div>
      <div class="contact-item"><div class="contact-icon">✉️</div><a href="mailto:g.l.stickerei@gmail.com">g.l.stickerei@gmail.com</a></div>
      <div class="contact-item"><div class="contact-icon">📸</div><a href="https://instagram.com/gamal.lisa" target="_blank">@gamal.lisa</a></div>
      <div class="contact-item"><div class="contact-icon">📍</div><span>Allerheiligenplatz 13, 1200 Wien</span></div>
    </div>
    <div class="contact-form-wrap">
      <form action="https://formspree.io/f/xvzllqpj" method="POST">
        <div class="form-group"><label>Name</label><input type="text" name="name" required></div>
        <div class="form-group"><label>E-Mail</label><input type="email" name="email" required></div>
        <div class="form-group"><label>Nachricht</label><textarea name="message" rows="4" required></textarea></div>
        <button type="submit" class="form-submit">Senden</button>
      </form>
    </div>
  </div>
  <div class="map-wrap">
    <div id="map"></div>
  </div>
</section>

<footer>© 2026 G&L Stickerei Wien · Alle Rechte vorbehalten</footer>

<script src="https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.9.4/leaflet.min.js"></script>
<script>
  const menuToggle = document.getElementById('mobile-menu');
  const navList = document.getElementById('nav-list');
  menuToggle.addEventListener('click', () => navList.classList.toggle('active'));

  const map = L.map('map').setView([48.23592, 16.37255], 16);
  L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
    attribution: '© OpenStreetMap'
  }).addTo(map);
  L.marker([48.23592, 16.37255]).addTo(map)
    .bindPopup('G&L Stickerei<br>Allerheiligenplatz 13, 1200 Wien')
    .openPopup();
</script>
</body>
</html>
