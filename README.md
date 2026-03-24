# guru.nat
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Guru — Technology Lead</title>
  <style>
    *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }

    :root {
      --bg:         #090d18;
      --surface:    #101624;
      --surface2:   #18223a;
      --border:     rgba(255,255,255,0.06);
      --text:       #e8e4d8;
      --muted:      #6e788f;
      --gold:       #c9a84c;
      --gold-light: #e2c47a;
      --gold-dim:   rgba(201,168,76,0.13);
    }

    html { scroll-behavior: smooth; }

    body {
      font-family: -apple-system, 'Helvetica Neue', sans-serif;
      background: var(--bg);
      color: var(--text);
      overflow-x: hidden;
    }

    nav {
      position: fixed;
      top: 0; left: 0; right: 0;
      z-index: 100;
      background: rgba(9,13,24,0.9);
      backdrop-filter: blur(20px) saturate(160%);
      border-bottom: 1px solid var(--border);
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 0 48px;
      height: 52px;
    }

    .nav-name { font-size: 17px; font-weight: 600; color: var(--gold-light); letter-spacing: -0.2px; }
    .nav-links { display: flex; gap: 32px; list-style: none; }
    .nav-links a { text-decoration: none; font-size: 14px; color: var(--muted); transition: color 0.2s; }
    .nav-links a:hover { color: var(--text); }
    .nav-cta { font-size: 14px; color: var(--gold); font-weight: 500; text-decoration: none; transition: color 0.2s; }
    .nav-cta:hover { color: var(--gold-light); }

    .hero {
      min-height: 100vh;
      display: flex; flex-direction: column;
      align-items: center; justify-content: center;
      text-align: center;
      padding: 120px 24px 80px;
      background: var(--bg);
      position: relative; overflow: hidden;
    }

    .hero::before {
      content: '';
      position: absolute; top: -200px; left: 50%;
      transform: translateX(-50%);
      width: 800px; height: 800px;
      background: radial-gradient(ellipse, rgba(201,168,76,0.07) 0%, transparent 65%);
      pointer-events: none;
    }

    .hero::after {
      content: '';
      position: absolute; bottom: 0; left: 0; right: 0; height: 1px;
      background: linear-gradient(90deg, transparent, rgba(201,168,76,0.3), transparent);
    }

    .hero-eyebrow {
      font-size: 11px; font-weight: 700; letter-spacing: 0.16em;
      text-transform: uppercase; color: var(--gold);
      margin-bottom: 20px; opacity: 0;
      animation: fadeUp 0.8s 0.2s forwards;
    }

    .hero-name {
      font-size: clamp(52px, 8vw, 96px);
      font-weight: 700; letter-spacing: -0.035em; line-height: 1.03;
      color: var(--text); margin-bottom: 24px;
      opacity: 0; animation: fadeUp 0.8s 0.35s forwards;
    }

    .hero-sub {
      font-size: clamp(18px, 2.4vw, 24px);
      font-weight: 300; color: var(--muted);
      max-width: 620px; line-height: 1.5; margin-bottom: 48px;
      opacity: 0; animation: fadeUp 0.8s 0.5s forwards;
    }
    .hero-sub strong { color: var(--text); font-weight: 400; }

    .hero-buttons {
      display: flex; gap: 14px; justify-content: center; flex-wrap: wrap;
      opacity: 0; animation: fadeUp 0.8s 0.65s forwards;
    }

    .btn-primary {
      display: inline-flex; align-items: center;
      background: var(--gold); color: #090d18;
      padding: 13px 28px; border-radius: 980px;
      font-size: 16px; font-weight: 700; text-decoration: none;
      transition: background 0.2s, transform 0.15s;
    }
    .btn-primary:hover { background: var(--gold-light); transform: scale(1.02); }

    .btn-secondary {
      display: inline-flex; align-items: center;
      background: transparent; color: var(--gold);
      padding: 13px 28px; border-radius: 980px;
      font-size: 16px; font-weight: 500; text-decoration: none;
      border: 1.5px solid rgba(201,168,76,0.4);
      transition: background 0.2s, border-color 0.2s, transform 0.15s;
    }
    .btn-secondary:hover { background: var(--gold-dim); border-color: var(--gold); transform: scale(1.02); }

    .scroll-hint {
      position: absolute; bottom: 32px; left: 50%; transform: translateX(-50%);
      opacity: 0; animation: fadeUp 1s 1.2s forwards;
      display: flex; flex-direction: column; align-items: center; gap: 6px;
      color: var(--muted); font-size: 11px; letter-spacing: 0.1em; text-transform: uppercase;
    }
    .scroll-arrow {
      width: 14px; height: 14px;
      border-right: 1.5px solid var(--muted); border-bottom: 1.5px solid var(--muted);
      transform: rotate(45deg); animation: bounce 1.6s ease-in-out infinite;
    }

    section { padding: 120px 48px; }

    .section-label {
      font-size: 11px; font-weight: 700; letter-spacing: 0.14em;
      text-transform: uppercase; color: var(--gold); margin-bottom: 14px;
    }
    .section-title {
      font-size: clamp(30px, 4.5vw, 54px);
      font-weight: 700; letter-spacing: -0.025em; line-height: 1.08;
      color: var(--text); margin-bottom: 20px;
    }
    .section-body {
      font-size: 18px; font-weight: 300; color: var(--muted);
      line-height: 1.65; max-width: 560px;
    }

    #about { background: var(--surface); }

    .about-grid {
      display: grid; grid-template-columns: 1fr 1fr;
      gap: 80px; align-items: center;
      max-width: 1100px; margin: 0 auto;
    }

    .about-stats {
      display: grid; grid-template-columns: 1fr 1fr;
      gap: 2px; margin-top: 48px;
    }

    .stat-card { background: var(--bg); padding: 28px 24px; border-radius: 2px; }
    .stat-card:first-child  { border-radius: 18px 2px 2px 2px; }
    .stat-card:nth-child(2) { border-radius: 2px 18px 2px 2px; }
    .stat-card:nth-child(3) { border-radius: 2px 2px 2px 18px; }
    .stat-card:last-child   { border-radius: 2px 2px 18px 2px; }

    .stat-number { font-size: 40px; font-weight: 700; letter-spacing: -0.03em; color: var(--text); line-height: 1; margin-bottom: 4px; }
    .stat-number em { font-size: 22px; font-style: normal; color: var(--gold); }
    .stat-desc { font-size: 13px; color: var(--muted); }

    .about-photo {
      width: 100%; aspect-ratio: 3/4;
      background: linear-gradient(145deg, #18223a, #101624);
      border-radius: 20px; border: 1px solid var(--border);
      display: flex; align-items: center; justify-content: center;
      position: relative; overflow: hidden;
    }
    .about-photo::before {
      content: ''; position: absolute; top: 0; left: 0; right: 0; height: 1px;
      background: linear-gradient(90deg, transparent, rgba(201,168,76,0.5), transparent);
    }
    .photo-placeholder { font-size: 72px; user-select: none; }
    .photo-badge {
      position: absolute; bottom: 20px; left: 20px; right: 20px;
      background: rgba(9,13,24,0.92); backdrop-filter: blur(14px);
      border-radius: 14px; padding: 14px 18px;
      border: 1px solid rgba(201,168,76,0.18);
    }
    .photo-badge-name { font-size: 15px; font-weight: 600; color: var(--gold-light); }
    .photo-badge-title { font-size: 13px; color: var(--muted); margin-top: 2px; }

    #expertise { background: var(--bg); text-align: center; }
    .expertise-intro { max-width: 680px; margin: 0 auto 72px; }
    .expertise-intro .section-body { margin: 0 auto; }

    .cards-grid {
      display: grid; grid-template-columns: repeat(3, 1fr);
      gap: 2px; max-width: 1100px; margin: 0 auto;
    }
    .card { background: var(--surface); padding: 40px 36px; text-align: left; transition: background 0.2s; }
    .card:hover { background: var(--surface2); }
    .card:first-child  { border-radius: 20px 2px 2px 2px; }
    .card:nth-child(3) { border-radius: 2px 20px 2px 2px; }
    .card:nth-child(4) { border-radius: 2px 2px 2px 20px; }
    .card:last-child   { border-radius: 2px 2px 20px 2px; }
    .card-icon { font-size: 30px; margin-bottom: 18px; }
    .card-title { font-size: 18px; font-weight: 600; color: var(--text); letter-spacing: -0.015em; margin-bottom: 10px; }
    .card-body { font-size: 14px; color: var(--muted); line-height: 1.6; }

    #projects { background: var(--surface); }
    .projects-header {
      max-width: 1100px; margin: 0 auto 56px;
      display: flex; justify-content: space-between; align-items: flex-end; gap: 24px;
    }
    .projects-grid {
      display: grid; grid-template-columns: 2fr 1fr;
      gap: 2px; max-width: 1100px; margin: 0 auto;
    }
    .project-card {
      background: var(--surface2); padding: 40px; border-radius: 2px;
      transition: background 0.2s; position: relative; overflow: hidden;
      min-height: 260px; display: flex; flex-direction: column; justify-content: space-between;
    }
    .project-card:hover { background: #1e2d4a; }
    .project-card:first-child  { border-radius: 20px 2px 2px 2px; }
    .project-card:nth-child(2) { border-radius: 2px 20px 20px 2px; }
    .project-card::before {
      content: ''; position: absolute; top: 0; left: 0; right: 0; height: 2px;
      background: linear-gradient(90deg, var(--gold), transparent 60%);
    }
    .project-tag { display: inline-block; font-size: 11px; font-weight: 700; letter-spacing: 0.1em; text-transform: uppercase; color: var(--gold); margin-bottom: 16px; }
    .project-title { font-size: 21px; font-weight: 600; color: var(--text); letter-spacing: -0.015em; margin-bottom: 12px; }
    .project-desc { font-size: 14px; color: var(--muted); line-height: 1.6; flex: 1; }
    .project-footer { margin-top: 28px; display: flex; align-items: center; gap: 16px; }
    .project-tech { display: flex; gap: 8px; flex-wrap: wrap; }
    .tech-pill {
      font-size: 12px; padding: 4px 12px; border-radius: 980px;
      background: var(--gold-dim); color: var(--gold-light);
      border: 1px solid rgba(201,168,76,0.2);
    }
    .project-link { margin-left: auto; font-size: 14px; color: var(--gold); text-decoration: none; white-space: nowrap; font-weight: 500; transition: color 0.2s; }
    .project-link:hover { color: var(--gold-light); }

    #contact { background: var(--bg); text-align: center; }
    .contact-inner { max-width: 620px; margin: 0 auto; }
    .contact-inner .section-body { margin: 0 auto 48px; }
    .contact-links { display: flex; gap: 14px; justify-content: center; flex-wrap: wrap; }
    .contact-link {
      display: flex; align-items: center; gap: 8px;
      padding: 14px 22px; background: var(--surface); border-radius: 14px;
      text-decoration: none; color: var(--text); font-size: 15px; font-weight: 500;
      border: 1px solid var(--border);
      transition: border-color 0.2s, transform 0.15s, box-shadow 0.2s;
    }
    .contact-link:hover {
      border-color: rgba(201,168,76,0.35);
      box-shadow: 0 4px 24px rgba(201,168,76,0.08);
      transform: translateY(-2px);
    }
    .contact-icon { font-size: 17px; }

    footer {
      background: var(--surface); border-top: 1px solid var(--border);
      padding: 22px 48px; display: flex; justify-content: space-between; align-items: center;
    }
    .footer-copy { font-size: 13px; color: var(--muted); }
    .footer-links { display: flex; gap: 24px; }
    .footer-links a { font-size: 13px; color: var(--muted); text-decoration: none; transition: color 0.2s; }
    .footer-links a:hover { color: var(--gold); }

    @keyframes fadeUp {
      from { opacity: 0; transform: translateY(24px); }
      to   { opacity: 1; transform: translateY(0); }
    }
    @keyframes bounce {
      0%, 100% { transform: rotate(45deg) translateY(0); }
      50%       { transform: rotate(45deg) translateY(5px); }
    }
    .reveal { opacity: 0; transform: translateY(28px); transition: opacity 0.7s ease, transform 0.7s ease; }
    .reveal.visible { opacity: 1; transform: none; }

    @media (max-width: 768px) {
      nav { padding: 0 24px; }
      .nav-links { display: none; }
      section { padding: 80px 24px; }
      .about-grid { grid-template-columns: 1fr; gap: 48px; }
      .cards-grid { grid-template-columns: 1fr; }
      .card { border-radius: 18px !important; }
      .projects-grid { grid-template-columns: 1fr; }
      .project-card { border-radius: 18px !important; }
      .projects-header { flex-direction: column; align-items: flex-start; }
      footer { flex-direction: column; gap: 12px; text-align: center; }
    }
  </style>
</head>
<body>

  <nav>
    <span class="nav-name">Guru</span>
    <ul class="nav-links">
      <li><a href="#about">About</a></li>
      <li><a href="#expertise">Expertise</a></li>
      <li><a href="#projects">Projects</a></li>
      <li><a href="#contact">Contact</a></li>
    </ul>
    <a href="mailto:hello@guru.dev" class="nav-cta">Get in touch ↗</a>
  </nav>

  <section class="hero">
    <p class="hero-eyebrow">Technology Lead &middot; Toronto, ON</p>
    <h1 class="hero-name">Guru</h1>
    <p class="hero-sub">
      15+ years building <strong>enterprise legal technology platforms</strong>
      and leading cloud migrations that actually ship.
    </p>
    <div class="hero-buttons">
      <a href="#projects" class="btn-primary">View Projects</a>
      <a href="#contact" class="btn-secondary">Download Resume</a>
    </div>
    <div class="scroll-hint">
      <span>Scroll</span>
      <div class="scroll-arrow"></div>
    </div>
  </section>

  <section id="about">
    <div class="about-grid">
      <div class="reveal">
        <p class="section-label">About</p>
        <h2 class="section-title">Built on depth,<br>not just breadth.</h2>
        <p class="section-body">
          I'm a Technology Lead at Info Tech with over 15 years in enterprise IT.
          My focus has been end-to-end legal technology — from architecting
          TeamConnect and iManage implementations to leading a full cloud migration to Microsoft Azure.
        </p>
        <div class="about-stats">
          <div class="stat-card"><div class="stat-number">15<em>+</em></div><div class="stat-desc">Years in Enterprise IT</div></div>
          <div class="stat-card"><div class="stat-number">4</div><div class="stat-desc">Core Platforms Delivered</div></div>
          <div class="stat-card"><div class="stat-number">1</div><div class="stat-desc">Full Azure Migration</div></div>
          <div class="stat-card"><div class="stat-number">∞</div><div class="stat-desc">Problems Enjoyed</div></div>
        </div>
      </div>
      <div class="about-photo reveal" style="transition-delay:0.15s">
        <div class="photo-placeholder">👤</div>
        <div class="photo-badge">
          <div class="photo-badge-name">Guru</div>
          <div class="photo-badge-title">Technology Lead · Info Tech</div>
        </div>
      </div>
    </div>
  </section>

  <section id="expertise">
    <div class="expertise-intro reveal">
      <p class="section-label">Expertise</p>
      <h2 class="section-title">What I bring to the table.</h2>
      <p class="section-body">From implementation to strategy, I operate across the full stack of legal technology management.</p>
    </div>
    <div class="cards-grid">
      <div class="card reveal"><div class="card-icon">⚖️</div><div class="card-title">Legal Technology Platforms</div><div class="card-body">Deep hands-on experience with Mitratech TeamConnect, Law Manager, iManage, and SharePoint DMS — from configuration to enterprise rollout.</div></div>
      <div class="card reveal" style="transition-delay:0.1s"><div class="card-icon">☁️</div><div class="card-title">Cloud & Infrastructure</div><div class="card-body">Led a major cloud migration to Microsoft Azure. Comfortable working across architecture, planning, and execution in hybrid enterprise environments.</div></div>
      <div class="card reveal" style="transition-delay:0.2s"><div class="card-icon">📋</div><div class="card-title">Project & Program Management</div><div class="card-body">End-to-end project ownership across enterprise legal platforms for large CPG clients. Currently pursuing PMP certification.</div></div>
      <div class="card reveal" style="transition-delay:0.05s"><div class="card-icon">🗄️</div><div class="card-title">Data & SQL</div><div class="card-body">Proficient in MS SQL Server — from complex multi-table UPDATE queries to transaction log management and performance tuning.</div></div>
      <div class="card reveal" style="transition-delay:0.15s"><div class="card-icon">🤖</div><div class="card-title">AI & Emerging Tech</div><div class="card-body">Actively upskilling in agentic AI for the banking and legal sectors, including PMI CPMAI and FinTech certifications.</div></div>
      <div class="card reveal" style="transition-delay:0.25s"><div class="card-icon">🔗</div><div class="card-title">Stakeholder Enablement</div><div class="card-body">Translating complex technical requirements into business value — bridging legal, IT, and executive stakeholders throughout the delivery lifecycle.</div></div>
    </div>
  </section>

  <section id="projects">
    <div class="projects-header reveal">
      <div>
        <p class="section-label">Projects</p>
        <h2 class="section-title">Things I've built.</h2>
      </div>
      <a href="#" class="btn-secondary" style="white-space:nowrap">View all →</a>
    </div>
    <div class="projects-grid">
      <div class="project-card reveal">
        <div>
          <span class="project-tag">Legal Tech · Azure</span>
          <div class="project-title">Enterprise Cloud Migration</div>
          <div class="project-desc">Led the end-to-end migration of a large CPG client's legal technology stack to Microsoft Azure — including TeamConnect, iManage, and associated integrations. Managed stakeholder alignment, vendor coordination, and cutover execution.</div>
        </div>
        <div class="project-footer">
          <div class="project-tech">
            <span class="tech-pill">Azure</span>
            <span class="tech-pill">TeamConnect</span>
            <span class="tech-pill">iManage</span>
          </div>
          <a href="#" class="project-link">View ↗</a>
        </div>
      </div>
      <div class="project-card reveal" style="transition-delay:0.15s">
        <div>
          <span class="project-tag">Coming Soon</span>
          <div class="project-title">Your Next Project</div>
          <div class="project-desc">This is where your hobby project goes — a side build, a tool, an experiment. Something that shows you build things, not just manage them.</div>
        </div>
        <div class="project-footer">
          <div class="project-tech"><span class="tech-pill">TBD</span></div>
        </div>
      </div>
    </div>
  </section>

  <section id="contact">
    <div class="contact-inner reveal">
      <p class="section-label">Contact</p>
      <h2 class="section-title">Let's connect.</h2>
      <p class="section-body">Open to new opportunities in legal technology management, enterprise platforms, and IT leadership.</p>
      <div class="contact-links">
        <a href="mailto:hello@guru.dev" class="contact-link"><span class="contact-icon">✉️</span> Email</a>
        <a href="https://linkedin.com" class="contact-link"><span class="contact-icon">💼</span> LinkedIn</a>
        <a href="https://github.com" class="contact-link"><span class="contact-icon">🐙</span> GitHub</a>
        <a href="#" class="contact-link"><span class="contact-icon">📄</span> Resume</a>
      </div>
    </div>
  </section>

  <footer>
    <span class="footer-copy">© 2026 Guru. All rights reserved.</span>
    <div class="footer-links">
      <a href="#about">About</a>
      <a href="#expertise">Expertise</a>
      <a href="#projects">Projects</a>
    </div>
  </footer>

  <script>
    const reveals = document.querySelectorAll('.reveal');
    const observer = new IntersectionObserver(entries => {
      entries.forEach(e => { if (e.isIntersecting) { e.target.classList.add('visible'); observer.unobserve(e.target); } });
    }, { threshold: 0.1 });
    reveals.forEach(el => observer.observe(el));
  </script>
</body>
</html>
