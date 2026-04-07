<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Gabriel Blanckaert — Développeur Fullstack</title>
<link href="https://fonts.googleapis.com/css2?family=DM+Serif+Display:ital@0;1&family=DM+Mono:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --bg: #0d0d0d;
    --bg2: #141414;
    --bg3: #1c1c1c;
    --line: rgba(255,255,255,0.07);
    --line2: rgba(255,255,255,0.14);
    --text: #f0ede6;
    --muted: #7a7872;
    --accent: #c8b97a;
    --accent2: #8ab4a0;
    --red: #c87a7a;
  }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'DM Mono', monospace;
    font-size: 13px;
    line-height: 1.7;
    overflow-x: hidden;
  }

  /* ── NOISE OVERLAY ── */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.035'/%3E%3C/svg%3E");
    pointer-events: none;
    z-index: 1000;
    opacity: 0.6;
  }

  /* ── GRID LINES ── */
  body::after {
    content: '';
    position: fixed;
    inset: 0;
    background-image: 
      linear-gradient(var(--line) 1px, transparent 1px),
      linear-gradient(90deg, var(--line) 1px, transparent 1px);
    background-size: 80px 80px;
    pointer-events: none;
    z-index: 0;
  }

  /* ── LAYOUT ── */
  .page { position: relative; z-index: 1; max-width: 900px; margin: 0 auto; padding: 0 40px; }

  /* ── HEADER ── */
  header {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    padding: 80px 0 60px;
    position: relative;
  }

  .header-index {
    font-size: 11px;
    color: var(--muted);
    letter-spacing: 0.15em;
    text-transform: uppercase;
    margin-bottom: 48px;
    display: flex;
    align-items: center;
    gap: 16px;
  }
  .header-index::before {
    content: '';
    display: block;
    width: 32px;
    height: 1px;
    background: var(--muted);
  }

  h1 {
    font-family: 'DM Serif Display', serif;
    font-size: clamp(52px, 9vw, 96px);
    font-weight: 400;
    line-height: 0.95;
    letter-spacing: -0.02em;
    color: var(--text);
    margin-bottom: 8px;
  }

  h1 em {
    font-style: italic;
    color: var(--accent);
  }

  .tagline {
    font-size: 12px;
    color: var(--muted);
    letter-spacing: 0.12em;
    text-transform: uppercase;
    margin-top: 24px;
    margin-bottom: 48px;
  }

  .header-bio {
    max-width: 520px;
    font-size: 14px;
    color: var(--muted);
    line-height: 1.8;
    border-left: 1px solid var(--line2);
    padding-left: 20px;
    margin-bottom: 48px;
  }

  .header-meta {
    display: flex;
    gap: 32px;
    flex-wrap: wrap;
  }

  .meta-item {
    display: flex;
    flex-direction: column;
    gap: 4px;
  }
  .meta-label {
    font-size: 10px;
    color: var(--muted);
    letter-spacing: 0.12em;
    text-transform: uppercase;
  }
  .meta-val {
    font-size: 13px;
    color: var(--text);
  }
  .meta-val a {
    color: var(--accent);
    text-decoration: none;
  }
  .meta-val a:hover { text-decoration: underline; }

  .scroll-hint {
    position: absolute;
    bottom: 40px;
    left: 0;
    display: flex;
    align-items: center;
    gap: 10px;
    font-size: 11px;
    color: var(--muted);
    letter-spacing: 0.1em;
  }
  .scroll-hint::after {
    content: '';
    display: block;
    width: 1px;
    height: 40px;
    background: linear-gradient(to bottom, var(--muted), transparent);
    animation: pulse 2s ease-in-out infinite;
  }
  @keyframes pulse { 0%,100%{opacity:0.4} 50%{opacity:1} }

  /* ── SECTION ── */
  section {
    padding: 80px 0;
    border-top: 1px solid var(--line);
  }

  .sec-header {
    display: flex;
    align-items: baseline;
    gap: 16px;
    margin-bottom: 48px;
  }

  .sec-num {
    font-size: 11px;
    color: var(--muted);
    letter-spacing: 0.1em;
    min-width: 28px;
  }

  h2 {
    font-family: 'DM Serif Display', serif;
    font-size: 32px;
    font-weight: 400;
    letter-spacing: -0.01em;
    color: var(--text);
  }

  /* ── SKILLS GRID ── */
  .skills-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 1px;
    background: var(--line);
    border: 1px solid var(--line);
  }

  .skill-cat {
    background: var(--bg2);
    padding: 28px;
    transition: background 0.2s;
  }
  .skill-cat:hover { background: var(--bg3); }

  .skill-cat-title {
    font-size: 10px;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    color: var(--accent);
    margin-bottom: 16px;
  }

  .skill-list {
    list-style: none;
    display: flex;
    flex-direction: column;
    gap: 6px;
  }

  .skill-list li {
    font-size: 13px;
    color: var(--text);
    display: flex;
    align-items: center;
    gap: 8px;
  }

  .skill-list li::before {
    content: '';
    display: block;
    width: 3px;
    height: 3px;
    background: var(--accent2);
    border-radius: 50%;
    flex-shrink: 0;
  }

  /* ── PROJECTS ── */
  .projects { display: flex; flex-direction: column; gap: 1px; background: var(--line); border: 1px solid var(--line); }

  .project {
    background: var(--bg2);
    padding: 32px 36px;
    display: grid;
    grid-template-columns: 1fr auto;
    gap: 24px;
    align-items: start;
    transition: background 0.2s;
    cursor: default;
  }
  .project:hover { background: var(--bg3); }

  .project-year {
    font-size: 11px;
    color: var(--muted);
    letter-spacing: 0.08em;
    margin-bottom: 6px;
  }

  .project-title {
    font-family: 'DM Serif Display', serif;
    font-size: 22px;
    font-weight: 400;
    color: var(--text);
    margin-bottom: 10px;
  }

  .project-desc {
    font-size: 13px;
    color: var(--muted);
    max-width: 500px;
    line-height: 1.7;
    margin-bottom: 14px;
  }

  .project-tags {
    display: flex;
    flex-wrap: wrap;
    gap: 6px;
  }

  .tag {
    font-size: 10px;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    padding: 3px 10px;
    border: 1px solid var(--line2);
    color: var(--muted);
  }

  .tag.highlight {
    border-color: var(--accent);
    color: var(--accent);
  }

  .project-badge {
    font-size: 10px;
    letter-spacing: 0.08em;
    color: var(--muted);
    text-align: right;
    white-space: nowrap;
  }
  .project-badge span {
    display: block;
    font-size: 18px;
    color: var(--text);
    font-family: 'DM Serif Display', serif;
    font-weight: 400;
    margin-bottom: 2px;
  }

  /* ── EXPERIENCE ── */
  .exp-list { display: flex; flex-direction: column; gap: 0; }

  .exp-item {
    padding: 28px 0;
    border-bottom: 1px solid var(--line);
    display: grid;
    grid-template-columns: 140px 1fr;
    gap: 32px;
  }

  .exp-period {
    font-size: 11px;
    color: var(--muted);
    letter-spacing: 0.08em;
    padding-top: 2px;
  }

  .exp-title {
    font-size: 15px;
    color: var(--text);
    margin-bottom: 4px;
  }

  .exp-company {
    font-size: 12px;
    color: var(--accent2);
    margin-bottom: 8px;
  }

  .exp-desc {
    font-size: 12px;
    color: var(--muted);
  }

  /* ── LANGUAGES ── */
  .lang-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 1px;
    background: var(--line);
    border: 1px solid var(--line);
  }

  .lang-item {
    background: var(--bg2);
    padding: 24px 28px;
  }

  .lang-name {
    font-family: 'DM Serif Display', serif;
    font-size: 24px;
    color: var(--text);
    margin-bottom: 4px;
  }

  .lang-level {
    font-size: 11px;
    color: var(--accent);
    letter-spacing: 0.1em;
    text-transform: uppercase;
    margin-bottom: 8px;
  }

  .lang-bar {
    height: 2px;
    background: var(--line2);
    position: relative;
  }
  .lang-bar-fill {
    position: absolute;
    left: 0; top: 0; height: 100%;
    background: var(--accent);
  }

  /* ── FOOTER ── */
  footer {
    border-top: 1px solid var(--line);
    padding: 48px 0;
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: wrap;
    gap: 16px;
  }

  .footer-name {
    font-family: 'DM Serif Display', serif;
    font-size: 20px;
    color: var(--text);
  }

  .footer-links {
    display: flex;
    gap: 24px;
  }

  .footer-links a {
    font-size: 11px;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    color: var(--muted);
    text-decoration: none;
    transition: color 0.2s;
  }
  .footer-links a:hover { color: var(--accent); }

  /* ── ANIMATIONS ── */
  .fade-in {
    opacity: 0;
    transform: translateY(20px);
    transition: opacity 0.6s ease, transform 0.6s ease;
  }
  .fade-in.visible {
    opacity: 1;
    transform: translateY(0);
  }

  /* ── RESPONSIVE ── */
  @media (max-width: 640px) {
    .page { padding: 0 20px; }
    .skills-grid, .lang-grid { grid-template-columns: 1fr; }
    .project { grid-template-columns: 1fr; }
    .exp-item { grid-template-columns: 1fr; gap: 6px; }
    h1 { font-size: 48px; }
  }
</style>
</head>
<body>
<div class="page">

  <!-- HEADER -->
  <header>
    <div class="header-index">Portfolio — 2025</div>
    <h1>Gabriel<br><em>Blanckaert</em></h1>
    <p class="tagline">Développeur Fullstack · École CODA, Orléans</p>
    <p class="header-bio">
      Étudiant en 1ère année de Bachelor Développeur Fullstack, avec 3 ans de pratique technique via la filière STI2D option SIN. Passionné par le développement web et embarqué, je cherche à mettre mes compétences en pratique sur des projets ambitieux.
    </p>
    <div class="header-meta">
      <div class="meta-item">
        <span class="meta-label">Contact</span>
        <span class="meta-val"><a href="mailto:gabriel.blanckaert@codastudent.school">gabriel.blanckaert@codastudent.school</a></span>
      </div>
      <div class="meta-item">
        <span class="meta-label">Téléphone</span>
        <span class="meta-val">06 33 82 22 28</span>
      </div>
      <div class="meta-item">
        <span class="meta-label">GitHub</span>
        <span class="meta-val"><a href="https://github.com/blanckaertgabriel3-sketch" target="_blank">blanckaertgabriel3-sketch</a></span>
      </div>
      <div class="meta-item">
        <span class="meta-label">LinkedIn</span>
        <span class="meta-val"><a href="https://www.linkedin.com/in/gabriel-blanckaert-1a676b38a/" target="_blank">gabriel-blanckaert</a></span>
      </div>
    </div>
    <div class="scroll-hint">Scroll</div>
  </header>

  <!-- COMPÉTENCES -->
  <section class="fade-in">
    <div class="sec-header">
      <span class="sec-num">01</span>
      <h2>Compétences</h2>
    </div>
    <div class="skills-grid">
      <div class="skill-cat">
        <div class="skill-cat-title">Langages</div>
        <ul class="skill-list">
          <li>PHP</li>
          <li>Python</li>
          <li>Java</li>
          <li>C / C++</li>
          <li>JavaScript</li>
        </ul>
      </div>
      <div class="skill-cat">
        <div class="skill-cat-title">Front-end</div>
        <ul class="skill-list">
          <li>HTML5 / CSS3</li>
          <li>Intégration responsive</li>
          <li>UI / UX — Figma</li>
          <li>JavaFX (desktop)</li>
        </ul>
      </div>
      <div class="skill-cat">
        <div class="skill-cat-title">Back-end & Data</div>
        <ul class="skill-list">
          <li>POO</li>
          <li>SQL</li>
          <li>Serveur PHP</li>
        </ul>
      </div>
      <div class="skill-cat">
        <div class="skill-cat-title">Outils & Env.</div>
        <ul class="skill-list">
          <li>Git / GitHub</li>
          <li>Docker</li>
          <li>Linux / Shell</li>
          <li>Arduino IDE</li>
        </ul>
      </div>
      <div class="skill-cat">
        <div class="skill-cat-title">Embarqué</div>
        <ul class="skill-list">
          <li>Arduino</li>
          <li>Servomoteurs</li>
          <li>Capteurs / actionneurs</li>
          <li>Électronique de base</li>
        </ul>
      </div>
      <div class="skill-cat">
        <div class="skill-cat-title">Éthique & qualité</div>
        <ul class="skill-list">
          <li>Green IT</li>
          <li>Numérique responsable</li>
          <li>Accessibilité</li>
        </ul>
      </div>
    </div>
  </section>

  <!-- PROJETS -->
  <section class="fade-in">
    <div class="sec-header">
      <span class="sec-num">02</span>
      <h2>Projets</h2>
    </div>
    <div class="projects">

      <div class="project">
        <div>
          <div class="project-year">2025</div>
          <div class="project-title">Bataille Navale Multijoueur</div>
          <p class="project-desc">Jeu de bataille navale local multijoueur avec interface interactive, gestion serveur PHP et suivi des parties via base de données SQL. Développé entièrement sous Linux.</p>
          <div class="project-tags">
            <span class="tag highlight">HTML</span>
            <span class="tag highlight">CSS</span>
            <span class="tag highlight">PHP</span>
            <span class="tag highlight">SQL</span>
            <span class="tag">Groupe de 2</span>
            <span class="tag">Linux</span>
          </div>
        </div>
        <div class="project-badge"><span>01</span>Web App</div>
      </div>

      <div class="project">
        <div>
          <div class="project-year">2025</div>
          <div class="project-title">Pathfinding Project</div>
          <p class="project-desc">Implémentation de l'algorithme de Dijkstra en C pour trouver le plus court chemin dans un graphe à partir de fichiers texte. Développé entièrement sous Linux.</p>
          <div class="project-tags">
            <span class="tag highlight">C</span>
            <span class="tag highlight">Dijkstra</span>
            <span class="tag">Groupe de 2</span>
            <span class="tag">Linux</span>
          </div>
        </div>
        <div class="project-badge"><span>02</span>Algorithmie</div>
      </div>

      <div class="project">
        <div>
          <div class="project-year">2024</div>
          <div class="project-title">ElderKeyboard</div>
          <p class="project-desc">Boîtier USB personnalisé (boutons, potentiomètre rotatif, potentiomètre glissière) piloté par Arduino. Conçu pour simplifier l'utilisation d'un PC via des raccourcis physiques. Présenté devant jury — Bac STI2D.</p>
          <div class="project-tags">
            <span class="tag highlight">C++</span>
            <span class="tag highlight">Arduino</span>
            <span class="tag">Groupe de 4</span>
            <span class="tag">Jury STI2D</span>
          </div>
        </div>
        <div class="project-badge"><span>03</span>Embarqué</div>
      </div>

      <div class="project">
        <div>
          <div class="project-year">2023</div>
          <div class="project-title">Labyrinthe Psychomoteur</div>
          <p class="project-desc">Labyrinthe physique piloté par manette, contrôlant 2 servomoteurs (axes X et Y), conçu pour aider des personnes en rééducation psychomotrice à regagner en autonomie. Testé et validé par de vrais utilisateurs.</p>
          <div class="project-tags">
            <span class="tag highlight">C++</span>
            <span class="tag highlight">Arduino</span>
            <span class="tag">Groupe de 5</span>
            <span class="tag">Impact réel</span>
          </div>
        </div>
        <div class="project-badge"><span>04</span>Embarqué</div>
      </div>

    </div>
  </section>

  <!-- FORMATION & EXPÉRIENCES -->
  <section class="fade-in">
    <div class="sec-header">
      <span class="sec-num">03</span>
      <h2>Formation & Expériences</h2>
    </div>
    <div class="exp-list">

      <div class="exp-item">
        <span class="exp-period">2025 — 2028</span>
        <div>
          <div class="exp-title">Bachelor Développeur Fullstack</div>
          <div class="exp-company">École CODA — Orléans</div>
          <div class="exp-desc">Formation en développement web fullstack, algorithmie, bases de données et numérique responsable.</div>
        </div>
      </div>

      <div class="exp-item">
        <span class="exp-period">2024</span>
        <div>
          <div class="exp-title">Terminale STI2D — Option SIN</div>
          <div class="exp-company">Lycée Privé Sainte Croix Sainte Euverte — Orléans</div>
          <div class="exp-desc">3 ans de pratique technique : électronique, programmation embarquée (Arduino), gestion de projet.</div>
        </div>
      </div>

      <div class="exp-item">
        <span class="exp-period">2023</span>
        <div>
          <div class="exp-title">Stage découverte</div>
          <div class="exp-company">Centrale nucléaire de Dampierre-en-Burly</div>
          <div class="exp-desc">Observation de la production d'électricité et des protocoles de sécurité industrielle.</div>
        </div>
      </div>

      <div class="exp-item">
        <span class="exp-period">2021</span>
        <div>
          <div class="exp-title">Stage découverte</div>
          <div class="exp-company">Strudal — Engenville</div>
          <div class="exp-desc">Fabrication de béton armé préfabriqué et procédures de maintenance industrielle.</div>
        </div>
      </div>

    </div>
  </section>

  <!-- LANGUES -->
  <section class="fade-in">
    <div class="sec-header">
      <span class="sec-num">04</span>
      <h2>Langues</h2>
    </div>
    <div class="lang-grid">
      <div class="lang-item">
        <div class="lang-name">Français</div>
        <div class="lang-level">C2 — Langue maternelle</div>
        <div class="lang-bar"><div class="lang-bar-fill" style="width:100%"></div></div>
      </div>
      <div class="lang-item">
        <div class="lang-name">Anglais</div>
        <div class="lang-level">B2 — Intermédiaire</div>
        <div class="lang-bar"><div class="lang-bar-fill" style="width:66%"></div></div>
      </div>
      <div class="lang-item">
        <div class="lang-name">Espagnol</div>
        <div class="lang-level">B1 — Débutant</div>
        <div class="lang-bar"><div class="lang-bar-fill" style="width:40%"></div></div>
      </div>
    </div>
  </section>

  <!-- FOOTER -->
  <footer class="fade-in">
    <div class="footer-name">Gabriel Blanckaert</div>
    <div class="footer-links">
      <a href="mailto:gabriel.blanckaert@codastudent.school">Email</a>
      <a href="https://github.com/blanckaertgabriel3-sketch" target="_blank">GitHub</a>
      <a href="https://www.linkedin.com/in/gabriel-blanckaert-1a676b38a/" target="_blank">LinkedIn</a>
    </div>
  </footer>

</div>

<script>
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(e => {
      if (e.isIntersecting) {
        e.target.classList.add('visible');
        observer.unobserve(e.target);
      }
    });
  }, { threshold: 0.1 });

  document.querySelectorAll('.fade-in').forEach(el => observer.observe(el));
</script>
</body>
</html>