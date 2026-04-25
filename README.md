<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>TechLearn — Apprends le futur</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=DM+Mono:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #050a0f;
    --surface: #0d1520;
    --border: #1a2a3a;
    --accent: #00e5ff;
    --accent2: #7c3aed;
    --accent3: #10b981;
    --warn: #f59e0b;
    --text: #e2eaf4;
    --muted: #6b8099;
    --card: #0a1520;
  }
  * { margin: 0; padding: 0; box-sizing: border-box; }
  html { scroll-behavior: smooth; }
  body { background: var(--bg); color: var(--text); font-family: 'DM Mono', monospace; overflow-x: hidden; cursor: none; }
  .cursor { position: fixed; width: 12px; height: 12px; background: var(--accent); border-radius: 50%; pointer-events: none; z-index: 9999; mix-blend-mode: screen; }
  .cursor-ring { position: fixed; width: 36px; height: 36px; border: 1.5px solid var(--accent); border-radius: 50%; pointer-events: none; z-index: 9998; opacity: 0.5; }
  body::before { content: ''; position: fixed; inset: 0; background-image: linear-gradient(rgba(0,229,255,0.03) 1px, transparent 1px), linear-gradient(90deg, rgba(0,229,255,0.03) 1px, transparent 1px); background-size: 60px 60px; pointer-events: none; z-index: 0; }
  nav { position: fixed; top: 0; left: 0; right: 0; z-index: 100; display: flex; align-items: center; justify-content: space-between; padding: 20px 60px; background: rgba(5,10,15,0.85); backdrop-filter: blur(20px); border-bottom: 1px solid var(--border); }
  .logo { font-family: 'Syne', sans-serif; font-size: 22px; font-weight: 800; letter-spacing: -0.5px; }
  .logo span { color: var(--accent); }
  .nav-links { display: flex; gap: 36px; list-style: none; }
  .nav-links a { color: var(--muted); text-decoration: none; font-size: 13px; letter-spacing: 1px; text-transform: uppercase; transition: color 0.2s; }
  .nav-links a:hover { color: var(--accent); }
  .nav-cta { background: var(--accent); color: var(--bg); border: none; padding: 10px 24px; font-family: 'Syne', sans-serif; font-weight: 700; font-size: 13px; letter-spacing: 1px; cursor: none; transition: all 0.2s; clip-path: polygon(8px 0%, 100% 0%, calc(100% - 8px) 100%, 0% 100%); }
  .nav-cta:hover { background: #fff; transform: scale(1.04); }
  .hero { min-height: 100vh; display: flex; flex-direction: column; justify-content: center; padding: 120px 60px 80px; position: relative; overflow: hidden; }
  .hero-badge { display: inline-flex; align-items: center; gap: 8px; background: rgba(0,229,255,0.08); border: 1px solid rgba(0,229,255,0.2); padding: 6px 16px; font-size: 11px; letter-spacing: 2px; text-transform: uppercase; color: var(--accent); margin-bottom: 32px; width: fit-content; animation: fadeDown 0.8s ease forwards; }
  .hero-badge::before { content: ''; width: 6px; height: 6px; background: var(--accent); border-radius: 50%; animation: pulse 1.5s infinite; }
  @keyframes pulse { 0%, 100% { opacity: 1; transform: scale(1); } 50% { opacity: 0.4; transform: scale(0.8); } }
  .hero h1 { font-family: 'Syne', sans-serif; font-size: clamp(52px, 8vw, 110px); font-weight: 800; line-height: 0.9; letter-spacing: -3px; margin-bottom: 32px; animation: fadeUp 0.9s ease 0.2s both; }
  .hero h1 .line2 { display: block; color: transparent; -webkit-text-stroke: 1.5px var(--accent); }
  .hero h1 .line3 { display: block; background: linear-gradient(90deg, var(--accent), var(--accent2)); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
  .hero-sub { max-width: 520px; color: var(--muted); font-size: 15px; line-height: 1.8; margin-bottom: 48px; animation: fadeUp 0.9s ease 0.4s both; }
  .hero-actions { display: flex; gap: 20px; align-items: center; animation: fadeUp 0.9s ease 0.6s both; }
  .btn-primary { background: var(--accent); color: var(--bg); border: none; padding: 16px 36px; font-family: 'Syne', sans-serif; font-weight: 700; font-size: 14px; letter-spacing: 1px; cursor: none; transition: all 0.2s; position: relative; overflow: hidden; }
  .btn-primary:hover { opacity: 0.85; transform: scale(1.02); }
  .btn-ghost { background: transparent; color: var(--text); border: 1px solid var(--border); padding: 16px 36px; font-family: 'Syne', sans-serif; font-weight: 600; font-size: 14px; cursor: none; transition: all 0.2s; }
  .btn-ghost:hover { border-color: var(--accent); color: var(--accent); }
  .orb { position: absolute; border-radius: 50%; filter: blur(80px); opacity: 0.15; pointer-events: none; }
  .orb1 { width: 500px; height: 500px; background: var(--accent); top: -100px; right: -100px; animation: float 8s ease-in-out infinite; }
  .orb2 { width: 300px; height: 300px; background: var(--accent2); bottom: 0; left: 30%; animation: float 10s ease-in-out infinite reverse; }
  @keyframes float { 0%, 100% { transform: translateY(0px); } 50% { transform: translateY(-30px); } }
  .stats-bar { display: flex; gap: 60px; padding: 40px 60px; border-top: 1px solid var(--border); border-bottom: 1px solid var(--border); background: var(--surface); position: relative; z-index: 1; flex-wrap: wrap; }
  .stat { display: flex; flex-direction: column; gap: 4px; }
  .stat-num { font-family: 'Syne', sans-serif; font-size: 32px; font-weight: 800; color: var(--accent); }
  .stat-label { font-size: 11px; color: var(--muted); letter-spacing: 1px; text-transform: uppercase; }
  section { padding: 100px 60px; position: relative; z-index: 1; }
  .section-label { font-size: 11px; letter-spacing: 3px; text-transform: uppercase; color: var(--accent); margin-bottom: 16px; display: flex; align-items: center; gap: 12px; }
  .section-label::before { content: ''; display: block; width: 30px; height: 1px; background: var(--accent); }
  .section-title { font-family: 'Syne', sans-serif; font-size: clamp(32px, 4vw, 56px); font-weight: 800; letter-spacing: -2px; line-height: 1; margin-bottom: 60px; }
  .categories { display: grid; grid-template-columns: repeat(2, 1fr); gap: 2px; background: var(--border); }
  .cat-card { background: var(--card); padding: 48px; position: relative; overflow: hidden; transition: all 0.3s; cursor: none; }
  .cat-card::before { content: ''; position: absolute; inset: 0; opacity: 0; transition: opacity 0.3s; }
  .cat-card:hover::before { opacity: 1; }
  .cat-card:hover { transform: scale(1.01); z-index: 2; }
  .cat-card.info::before { background: linear-gradient(135deg, rgba(0,229,255,0.06), transparent); }
  .cat-card.prog::before { background: linear-gradient(135deg, rgba(124,58,237,0.06), transparent); }
  .cat-card.cyber::before { background: linear-gradient(135deg, rgba(16,185,129,0.06), transparent); }
  .cat-card.ai::before { background: linear-gradient(135deg, rgba(245,158,11,0.06), transparent); }
  .cat-icon { font-size: 48px; margin-bottom: 24px; display: block; }
  .cat-number { position: absolute; top: 24px; right: 24px; font-family: 'Syne', sans-serif; font-size: 64px; font-weight: 800; opacity: 0.04; color: white; line-height: 1; }
  .cat-title { font-family: 'Syne', sans-serif; font-size: 24px; font-weight: 700; margin-bottom: 12px; }
  .cat-desc { color: var(--muted); font-size: 13px; line-height: 1.7; margin-bottom: 28px; }
  .cat-tag { display: inline-block; padding: 4px 12px; font-size: 10px; letter-spacing: 1.5px; text-transform: uppercase; border: 1px solid; margin-right: 8px; margin-bottom: 8px; }
  .info .cat-tag { border-color: rgba(0,229,255,0.3); color: var(--accent); }
  .prog .cat-tag { border-color: rgba(124,58,237,0.4); color: #a78bfa; }
  .cyber .cat-tag { border-color: rgba(16,185,129,0.3); color: var(--accent3); }
  .ai .cat-tag { border-color: rgba(245,158,11,0.3); color: var(--warn); }
  .cat-arrow { position: absolute; bottom: 36px; right: 36px; width: 40px; height: 40px; display: flex; align-items: center; justify-content: center; border: 1px solid var(--border); transition: all 0.3s; font-size: 18px; }
  .cat-card:hover .cat-arrow { border-color: var(--accent); color: var(--accent); transform: rotate(45deg); }
  .courses-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 20px; }
  .course-card { background: var(--card); border: 1px solid var(--border); padding: 28px; transition: all 0.3s; cursor: none; position: relative; overflow: hidden; }
  .course-card::after { content: ''; position: absolute; bottom: 0; left: 0; right: 0; height: 2px; transform: scaleX(0); transition: transform 0.3s; transform-origin: left; }
  .course-card.c1::after { background: var(--accent); }
  .course-card.c2::after { background: #a78bfa; }
  .course-card.c3::after { background: var(--accent3); }
  .course-card.c4::after { background: var(--warn); }
  .course-card.c5::after { background: var(--accent); }
  .course-card.c6::after { background: #a78bfa; }
  .course-card:hover::after { transform: scaleX(1); }
  .course-card:hover { border-color: rgba(255,255,255,0.1); transform: translateY(-4px); }
  .course-level { font-size: 10px; letter-spacing: 2px; text-transform: uppercase; margin-bottom: 16px; padding: 3px 10px; width: fit-content; display: inline-block; }
  .level-debut { background: rgba(16,185,129,0.15); color: var(--accent3); }
  .level-inter { background: rgba(245,158,11,0.15); color: var(--warn); }
  .level-avance { background: rgba(239,68,68,0.15); color: #f87171; }
  .course-title { font-family: 'Syne', sans-serif; font-size: 17px; font-weight: 700; margin-bottom: 10px; line-height: 1.3; }
  .course-meta { display: flex; gap: 16px; color: var(--muted); font-size: 12px; margin-top: 20px; padding-top: 16px; border-top: 1px solid var(--border); }
  .progress-bar { height: 2px; background: var(--border); margin-top: 14px; overflow: hidden; }
  .progress-fill { height: 100%; background: var(--accent); transition: width 1.2s ease; }
  .path-steps { display: grid; grid-template-columns: repeat(4, 1fr); gap: 40px; position: relative; }
  .path-steps::before { content: ''; position: absolute; top: 28px; left: 28px; right: 28px; height: 1px; background: linear-gradient(90deg, var(--accent), var(--accent2), var(--accent3)); z-index: 0; }
  .path-step { text-align: center; position: relative; z-index: 1; }
  .step-num { width: 56px; height: 56px; background: var(--bg); border: 1px solid var(--border); border-radius: 50%; display: flex; align-items: center; justify-content: center; margin: 0 auto 20px; font-family: 'Syne', sans-serif; font-weight: 700; font-size: 16px; }
  .path-step:nth-child(1) .step-num { border-color: var(--accent); color: var(--accent); }
  .path-step:nth-child(2) .step-num { border-color: #a78bfa; color: #a78bfa; }
  .path-step:nth-child(3) .step-num { border-color: var(--accent3); color: var(--accent3); }
  .path-step:nth-child(4) .step-num { border-color: var(--warn); color: var(--warn); }
  .step-title { font-family: 'Syne', sans-serif; font-weight: 700; margin-bottom: 8px; font-size: 14px; }
  .step-desc { color: var(--muted); font-size: 12px; line-height: 1.6; }
  .testimonials { display: grid; grid-template-columns: repeat(3, 1fr); gap: 20px; }
  .testi { background: var(--card); border: 1px solid var(--border); padding: 28px; position: relative; }
  .testi::before { content: '"'; font-family: 'Syne', sans-serif; font-size: 80px; color: var(--accent); opacity: 0.1; position: absolute; top: 10px; right: 20px; line-height: 1; }
  .testi-text { font-size: 13px; line-height: 1.8; color: var(--muted); margin-bottom: 20px; }
  .testi-name { font-family: 'Syne', sans-serif; font-weight: 700; font-size: 14px; }
  .testi-role { font-size: 11px; color: var(--muted); margin-top: 2px; }
  .cta-section { text-align: center; padding: 120px 60px; position: relative; overflow: hidden; }
  .cta-section::before { content: ''; position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%); width: 600px; height: 600px; background: radial-gradient(circle, rgba(0,229,255,0.06), transparent 70%); pointer-events: none; }
  .cta-title { font-family: 'Syne', sans-serif; font-size: clamp(40px, 6vw, 80px); font-weight: 800; letter-spacing: -3px; line-height: 1; margin-bottom: 24px; }
  .cta-sub { color: var(--muted); font-size: 15px; margin-bottom: 48px; }
  footer { border-top: 1px solid var(--border); padding: 40px 60px; display: flex; justify-content: space-between; align-items: center; background: var(--surface); }
  .footer-left, .footer-right { color: var(--muted); font-size: 12px; }
  @keyframes fadeUp { from { opacity: 0; transform: translateY(30px); } to { opacity: 1; transform: translateY(0); } }
  @keyframes fadeDown { from { opacity: 0; transform: translateY(-20px); } to { opacity: 1; transform: translateY(0); } }
  .reveal { opacity: 0; transform: translateY(30px); transition: opacity 0.7s ease, transform 0.7s ease; }
  .reveal.visible { opacity: 1; transform: translateY(0); }
  ::-webkit-scrollbar { width: 4px; }
  ::-webkit-scrollbar-track { background: var(--bg); }
  ::-webkit-scrollbar-thumb { background: var(--border); }
  ::-webkit-scrollbar-thumb:hover { background: var(--accent); }
  @media (max-width: 768px) {
    nav { padding: 16px 24px; }
    .nav-links { display: none; }
    .hero, section { padding: 80px 24px 60px; }
    .stats-bar { padding: 30px 24px; gap: 30px; }
    .categories, .courses-grid, .testimonials { grid-template-columns: 1fr; }
    .path-steps { grid-template-columns: 1fr 1fr; }
    .path-steps::before { display: none; }
    footer { flex-direction: column; gap: 12px; text-align: center; padding: 30px 24px; }
  }
</style>
</head>
<body>

<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursorRing"></div>

<nav>
  <div class="logo">TECH<span>LEARN</span></div>
  <ul class="nav-links">
    <li><a href="#categories">Catégories</a></li>
    <li><a href="#courses">Cours</a></li>
    <li><a href="#parcours">Parcours</a></li>
    <li><a href="#temoignages">Témoignages</a></li>
  </ul>
  <button class="nav-cta">Commencer</button>
</nav>

<section class="hero">
  <div class="orb orb1"></div>
  <div class="orb orb2"></div>
  <div class="hero-badge">🟢 Plateforme active — 12 400 apprenants</div>
  <h1>
    Maîtrise<br>
    <span class="line2">le code,</span>
    <span class="line3">le futur.</span>
  </h1>
  <p class="hero-sub">
    Informatique, programmation, cybersécurité, intelligence artificielle — tout ce dont tu as besoin pour devenir expert du numérique, en un seul endroit.
  </p>
  <div class="hero-actions">
    <button class="btn-primary">→ Commencer gratuitement</button>
    <button class="btn-ghost">Voir les cours</button>
  </div>
</section>

<div class="stats-bar">
  <div class="stat"><span class="stat-num" data-target="240">0</span><span class="stat-label">Cours disponibles</span></div>
  <div class="stat"><span class="stat-num" data-target="12400">0</span><span class="stat-label">Apprenants actifs</span></div>
  <div class="stat"><span class="stat-num" data-target="4">0</span><span class="stat-label">Domaines couverts</span></div>
  <div class="stat"><span class="stat-num" data-target="98">0</span><span class="stat-label">% Satisfaction</span></div>
</div>

<section id="categories">
  <div class="section-label">Ce qu'on couvre</div>
  <h2 class="section-title reveal">4 domaines.<br>Un seul objectif.</h2>
  <div class="categories reveal">
    <div class="cat-card info">
      <span class="cat-number">01</span>
      <span class="cat-icon">🖥️</span>
      <div class="cat-title">Informatique</div>
      <p class="cat-desc">Les fondations : réseaux, systèmes d'exploitation, hardware, logique binaire. Comprends comment tout fonctionne sous le capot.</p>
      <div><span class="cat-tag">Réseaux</span><span class="cat-tag">Linux</span><span class="cat-tag">Hardware</span><span class="cat-tag">Binaire</span></div>
      <div class="cat-arrow">↗</div>
    </div>
    <div class="cat-card prog">
      <span class="cat-number">02</span>
      <span class="cat-icon">⌨️</span>
      <div class="cat-title">Programmation</div>
      <p class="cat-desc">Python, JavaScript, C++, Java, Rust — maîtrise les langages les plus demandés et crée tes propres applications.</p>
      <div><span class="cat-tag">Python</span><span class="cat-tag">JavaScript</span><span class="cat-tag">C++</span><span class="cat-tag">Java</span></div>
      <div class="cat-arrow">↗</div>
    </div>
    <div class="cat-card cyber">
      <span class="cat-number">03</span>
      <span class="cat-icon">🔐</span>
      <div class="cat-title">Cybersécurité</div>
      <p class="cat-desc">Ethical hacking, cryptographie, sécurité des réseaux, CTF challenges. Deviens le gardien du monde numérique.</p>
      <div><span class="cat-tag">Ethical Hacking</span><span class="cat-tag">Crypto</span><span class="cat-tag">CTF</span><span class="cat-tag">OSINT</span></div>
      <div class="cat-arrow">↗</div>
    </div>
    <div class="cat-card ai">
      <span class="cat-number">04</span>
      <span class="cat-icon">🤖</span>
      <div class="cat-title">Intelligence Artificielle</div>
      <p class="cat-desc">Machine learning, deep learning, NLP, computer vision. Construis les systèmes qui vont changer le monde demain.</p>
      <div><span class="cat-tag">Machine Learning</span><span class="cat-tag">Deep Learning</span><span class="cat-tag">NLP</span><span class="cat-tag">TensorFlow</span></div>
      <div class="cat-arrow">↗</div>
    </div>
  </div>
</section>

<section id="courses" style="background: var(--surface); border-top: 1px solid var(--border); border-bottom: 1px solid var(--border);">
  <div class="section-label">Catalogue</div>
  <h2 class="section-title reveal">Cours populaires</h2>
  <div class="courses-grid reveal">
    <div class="course-card c1">
      <span class="course-level level-debut">Débutant</span>
      <div class="course-title">Python — De zéro à héros</div>
      <p style="color:var(--muted);font-size:12px;line-height:1.6">Variables, fonctions, POO, bibliothèques. Ton premier langage complet.</p>
      <div class="progress-bar"><div class="progress-fill" data-width="85%"></div></div>
      <div class="course-meta"><span>⏱ 24h</span><span>📚 48 leçons</span><span>⭐ 4.9</span></div>
    </div>
    <div class="course-card c2">
      <span class="course-level level-inter">Intermédiaire</span>
      <div class="course-title">JavaScript — Web moderne</div>
      <p style="color:var(--muted);font-size:12px;line-height:1.6">ES6+, React, Node.js, APIs REST. Crée des sites web interactifs.</p>
      <div class="progress-bar"><div class="progress-fill" data-width="72%" style="background:#a78bfa"></div></div>
      <div class="course-meta"><span>⏱ 32h</span><span>📚 60 leçons</span><span>⭐ 4.8</span></div>
    </div>
    <div class="course-card c3">
      <span class="course-level level-debut">Débutant</span>
      <div class="course-title">Linux & Ligne de commande</div>
      <p style="color:var(--muted);font-size:12px;line-height:1.6">Terminal, scripts bash, gestion de fichiers, permissions et processus.</p>
      <div class="progress-bar"><div class="progress-fill" data-width="60%" style="background:var(--accent3)"></div></div>
      <div class="course-meta"><span>⏱ 16h</span><span>📚 32 leçons</span><span>⭐ 4.7</span></div>
    </div>
    <div class="course-card c4">
      <span class="course-level level-avance">Avancé</span>
      <div class="course-title">Ethical Hacking — CTF Bootcamp</div>
      <p style="color:var(--muted);font-size:12px;line-height:1.6">Pentest, exploitation de vulnérabilités, Kali Linux, OWASP Top 10.</p>
      <div class="progress-bar"><div class="progress-fill" data-width="45%" style="background:var(--warn)"></div></div>
      <div class="course-meta"><span>⏱ 40h</span><span>📚 75 leçons</span><span>⭐ 4.9</span></div>
    </div>
    <div class="course-card c5">
      <span class="course-level level-inter">Intermédiaire</span>
      <div class="course-title">Machine Learning avec Python</div>
      <p style="color:var(--muted);font-size:12px;line-height:1.6">Scikit-learn, régression, classification, réseaux de neurones.</p>
      <div class="progress-bar"><div class="progress-fill" data-width="90%"></div></div>
      <div class="course-meta"><span>⏱ 28h</span><span>📚 52 leçons</span><span>⭐ 5.0</span></div>
    </div>
    <div class="course-card c6">
      <span class="course-level level-debut">Débutant</span>
      <div class="course-title">Réseaux & Protocoles TCP/IP</div>
      <p style="color:var(--muted);font-size:12px;line-height:1.6">Modèle OSI, IP, DNS, HTTP, Wireshark. Comprends internet de A à Z.</p>
      <div class="progress-bar"><div class="progress-fill" data-width="55%" style="background:#a78bfa"></div></div>
      <div class="course-meta"><span>⏱ 18h</span><span>📚 36 leçons</span><span>⭐ 4.6</span></div>
    </div>
  </div>
</section>

<section id="parcours">
  <div class="section-label">Chemin d'apprentissage</div>
  <h2 class="section-title reveal">Ton parcours<br>en 4 étapes</h2>
  <div class="path-steps reveal">
    <div class="path-step"><div class="step-num">01</div><div class="step-title">Choisis ton domaine</div><p class="step-desc">Informatique, code, cybersécurité ou IA — commence par ce qui t'attire.</p></div>
    <div class="path-step"><div class="step-num">02</div><div class="step-title">Suis le programme</div><p class="step-desc">Des cours structurés du niveau débutant à expert, à ton rythme.</p></div>
    <div class="path-step"><div class="step-num">03</div><div class="step-title">Pratique sur des projets</div><p class="step-desc">Applique tes connaissances sur de vrais projets et challenges.</p></div>
    <div class="path-step"><div class="step-num">04</div><div class="step-title">Obtiens ta certification</div><p class="step-desc">Un certificat validé par l'industrie pour booster ton profil.</p></div>
  </div>
</section>

<section id="temoignages" style="background:var(--surface);border-top:1px solid var(--border)">
  <div class="section-label">Communauté</div>
  <h2 class="section-title reveal">Ce qu'ils disent</h2>
  <div class="testimonials reveal">
    <div class="testi">
      <p class="testi-text">En 6 mois sur TechLearn, j'ai appris Python et décroché mon premier emploi de développeur. Les cours sont clairs, les projets pratiques, c'est exactement ce qu'il faut.</p>
      <div class="testi-name">Amadou K.</div><div class="testi-role">Développeur Python — Dakar</div>
    </div>
    <div class="testi">
      <p class="testi-text">La section cybersécurité m'a complètement transformé. J'ai réussi mon premier CTF en 3 mois. La communauté est incroyablement utile et motivante.</p>
      <div class="testi-name">Fatima Z.</div><div class="testi-role">Security Analyst — Casablanca</div>
    </div>
    <div class="testi">
      <p class="testi-text">Je suis arrivé avec zéro connaissance en informatique. Aujourd'hui je code mes propres modèles d'IA. TechLearn change vraiment des vies.</p>
      <div class="testi-name">Jean-Paul M.</div><div class="testi-role">ML Engineer — Abidjan</div>
    </div>
  </div>
</section>

<section class="cta-section">
  <h2 class="cta-title reveal">Prêt à coder<br>ton avenir ?</h2>
  <p class="cta-sub reveal">Rejoins 12 400+ apprenants qui construisent leur futur avec TechLearn.</p>
  <button class="btn-primary reveal" style="font-size:16px;padding:20px 48px">→ Commencer gratuitement</button>
</section>

<footer>
  <div class="footer-left">© 2026 TechLearn — Apprends le futur</div>
  <div class="footer-right">Informatique · Programmation · Cybersécurité · IA</div>
</footer>

<script>
  // Custom cursor
  const cursor = document.getElementById('cursor');
  const ring = document.getElementById('cursorRing');
  let mx = 0, my = 0, rx = 0, ry = 0;
  document.addEventListener('mousemove', e => { mx = e.clientX; my = e.clientY; });
  function animCursor() {
    cursor.style.left = (mx - 6) + 'px'; cursor.style.top = (my - 6) + 'px';
    rx += (mx - rx) * 0.12; ry += (my - ry) * 0.12;
    ring.style.left = (rx - 18) + 'px'; ring.style.top = (ry - 18) + 'px';
    requestAnimationFrame(animCursor);
  }
  animCursor();

  // Scroll reveal
  const observer = new IntersectionObserver(entries => {
    entries.forEach((e, i) => {
      if (e.isIntersecting) { e.target.style.transitionDelay = (i * 0.08) + 's'; e.target.classList.add('visible'); }
    });
  }, { threshold: 0.1 });
  document.querySelectorAll('.reveal').forEach(r => observer.observe(r));

  // Counters
  function animCounter(el, target) {
    let v = 0; const step = target / 120;
    const t = setInterval(() => {
      v = Math.min(v + step, target);
      el.textContent = Math.floor(v).toLocaleString('fr');
      if (v >= target) clearInterval(t);
    }, 16);
  }
  const statsObs = new IntersectionObserver(entries => {
    if (entries[0].isIntersecting) {
      document.querySelectorAll('[data-target]').forEach(el => animCounter(el, +el.dataset.target));
      statsObs.disconnect();
    }
  });
  statsObs.observe(document.querySelector('.stats-bar'));

  // Progress bars
  const progObs = new IntersectionObserver(entries => {
    entries.forEach(e => {
      if (e.isIntersecting) {
        e.target.querySelectorAll('.progress-fill').forEach(bar => {
          const w = bar.dataset.width;
          setTimeout(() => bar.style.width = w, 300);
        });
      }
    });
  }, { threshold: 0.2 });
  document.querySelectorAll('.courses-grid').forEach(g => progObs.observe(g));
</script>
</body>
</html>
