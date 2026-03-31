<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>CE-HACKATHON — README</title>
<link href="https://fonts.googleapis.com/css2?family=Space+Mono:wght@400;700&family=Syne:wght@400;600;700;800&display=swap" rel="stylesheet" />
<style>
  :root {
    --green: #00ff9d;
    --purple: #6c63ff;
    --dark: #0d0d0d;
    --darker: #080808;
    --card: #141414;
    --border: rgba(255,255,255,0.08);
    --text: #e8e8e8;
    --muted: #888;
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--darker);
    color: var(--text);
    font-family: 'Syne', sans-serif;
    overflow-x: hidden;
    cursor: none;
  }

  /* ─── Custom cursor ─── */
  .cursor {
    width: 12px; height: 12px;
    background: var(--green);
    border-radius: 50%;
    position: fixed; top: 0; left: 0;
    pointer-events: none; z-index: 9999;
    transform: translate(-50%,-50%);
    transition: transform 0.1s, background 0.2s;
    mix-blend-mode: difference;
  }
  .cursor-ring {
    width: 36px; height: 36px;
    border: 1px solid rgba(0,255,157,0.5);
    border-radius: 50%;
    position: fixed; top: 0; left: 0;
    pointer-events: none; z-index: 9998;
    transform: translate(-50%,-50%);
    transition: transform 0.18s ease, width 0.2s, height 0.2s;
  }

  /* ─── Scanline overlay ─── */
  body::before {
    content: '';
    position: fixed; inset: 0;
    background: repeating-linear-gradient(0deg, transparent, transparent 2px, rgba(0,0,0,0.03) 2px, rgba(0,0,0,0.03) 4px);
    pointer-events: none; z-index: 100;
  }

  /* ─── Canvas particles ─── */
  #particles { position: fixed; inset: 0; z-index: 0; pointer-events: none; }

  /* ─── HERO ─── */
  .hero {
    position: relative; z-index: 1;
    min-height: 100vh;
    display: flex; flex-direction: column;
    justify-content: center; align-items: center;
    text-align: center;
    padding: 2rem;
    overflow: hidden;
  }

  .hero-glow {
    position: absolute;
    width: 600px; height: 600px;
    border-radius: 50%;
    background: radial-gradient(circle, rgba(108,99,255,0.18) 0%, transparent 70%);
    top: 50%; left: 50%;
    transform: translate(-50%,-50%);
    animation: breathe 4s ease-in-out infinite;
  }

  @keyframes breathe {
    0%,100% { transform: translate(-50%,-50%) scale(1); opacity: 0.8; }
    50% { transform: translate(-50%,-50%) scale(1.15); opacity: 1; }
  }

  .badge {
    display: inline-flex; align-items: center; gap: 8px;
    background: rgba(0,255,157,0.08);
    border: 1px solid rgba(0,255,157,0.25);
    color: var(--green);
    font-family: 'Space Mono', monospace;
    font-size: 0.7rem;
    letter-spacing: 0.15em;
    padding: 6px 16px;
    border-radius: 100px;
    margin-bottom: 2rem;
    animation: fadeSlideDown 0.8s ease forwards;
    opacity: 0;
  }
  .badge-dot {
    width: 6px; height: 6px;
    background: var(--green);
    border-radius: 50%;
    animation: pulse 1.5s ease-in-out infinite;
  }
  @keyframes pulse { 0%,100%{opacity:1;transform:scale(1);} 50%{opacity:0.4;transform:scale(0.7);} }

  .hero-title {
    font-size: clamp(3rem, 10vw, 7rem);
    font-weight: 800;
    line-height: 1;
    letter-spacing: -0.03em;
    margin-bottom: 0.5rem;
    opacity: 0;
    animation: fadeSlideUp 1s 0.2s ease forwards;
  }
  .hero-title .line1 { display: block; color: #fff; }
  .hero-title .line2 {
    display: block;
    background: linear-gradient(90deg, var(--green), var(--purple));
    -webkit-background-clip: text; background-clip: text;
    -webkit-text-fill-color: transparent;
  }

  .hero-sub {
    font-size: 1.1rem; color: var(--muted);
    max-width: 520px;
    line-height: 1.7;
    opacity: 0;
    animation: fadeSlideUp 1s 0.4s ease forwards;
    margin-bottom: 2.5rem;
  }

  .hero-btns {
    display: flex; gap: 1rem; flex-wrap: wrap; justify-content: center;
    opacity: 0;
    animation: fadeSlideUp 1s 0.6s ease forwards;
    margin-bottom: 4rem;
  }

  .btn {
    padding: 14px 28px;
    border-radius: 8px;
    font-family: 'Space Mono', monospace;
    font-size: 0.82rem;
    font-weight: 700;
    letter-spacing: 0.04em;
    cursor: pointer;
    transition: transform 0.2s, box-shadow 0.2s;
    text-decoration: none;
    display: inline-flex; align-items: center; gap: 8px;
  }
  .btn-primary {
    background: linear-gradient(135deg, var(--green), #00d4ff);
    color: #000;
    border: none;
    box-shadow: 0 0 30px rgba(0,255,157,0.3);
  }
  .btn-primary:hover { transform: translateY(-3px); box-shadow: 0 0 50px rgba(0,255,157,0.5); }

  .btn-outline {
    background: transparent;
    color: var(--text);
    border: 1px solid var(--border);
  }
  .btn-outline:hover { border-color: var(--purple); color: var(--purple); transform: translateY(-3px); }

  /* Stats strip */
  .stats-strip {
    display: flex; gap: 2rem; flex-wrap: wrap; justify-content: center;
    opacity: 0;
    animation: fadeSlideUp 1s 0.8s ease forwards;
  }
  .stat { text-align: center; }
  .stat-num {
    font-family: 'Space Mono', monospace;
    font-size: 1.6rem;
    font-weight: 700;
    background: linear-gradient(90deg, var(--green), var(--purple));
    -webkit-background-clip: text; background-clip: text;
    -webkit-text-fill-color: transparent;
  }
  .stat-label { font-size: 0.75rem; color: var(--muted); margin-top: 2px; letter-spacing: 0.08em; }

  .stat-divider { width: 1px; background: var(--border); }

  /* ─── SCROLL INDICATOR ─── */
  .scroll-hint {
    position: absolute; bottom: 2rem;
    display: flex; flex-direction: column; align-items: center;
    gap: 8px; color: var(--muted);
    font-family: 'Space Mono', monospace;
    font-size: 0.65rem;
    letter-spacing: 0.1em;
    opacity: 0;
    animation: fadeSlideUp 1s 1s ease forwards;
  }
  .scroll-line {
    width: 1px; height: 40px;
    background: linear-gradient(to bottom, var(--green), transparent);
    animation: scrollLine 1.5s ease-in-out infinite;
  }
  @keyframes scrollLine { 0%,100%{transform:scaleY(1);opacity:1;} 50%{transform:scaleY(0.4);opacity:0.4;} }

  /* ─── COMMON SECTION ─── */
  section { position: relative; z-index: 1; padding: 6rem 2rem; }

  .section-label {
    font-family: 'Space Mono', monospace;
    font-size: 0.7rem;
    color: var(--green);
    letter-spacing: 0.2em;
    text-transform: uppercase;
    margin-bottom: 0.8rem;
  }

  .section-title {
    font-size: clamp(2rem, 4vw, 3rem);
    font-weight: 800;
    line-height: 1.15;
    letter-spacing: -0.02em;
  }

  .container { max-width: 1100px; margin: 0 auto; }

  /* ─── DIVIDER ─── */
  .divider {
    height: 1px;
    background: linear-gradient(90deg, transparent, var(--green), var(--purple), transparent);
    opacity: 0.3;
    margin: 0 2rem;
    position: relative; z-index: 1;
  }

  /* ─── ABOUT ─── */
  .about-grid {
    display: grid; grid-template-columns: 1fr 1fr;
    gap: 4rem; align-items: center;
    margin-top: 3rem;
  }
  .about-text p {
    color: var(--muted);
    line-height: 1.8;
    font-size: 1.05rem;
    margin-bottom: 1rem;
  }
  .about-text p span { color: var(--green); font-weight: 600; }

  .about-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 16px;
    padding: 2rem;
    position: relative; overflow: hidden;
  }
  .about-card::before {
    content: '';
    position: absolute; top: 0; left: 0; right: 0;
    height: 2px;
    background: linear-gradient(90deg, var(--green), var(--purple));
  }
  .tech-stack { display: flex; flex-wrap: wrap; gap: 10px; margin-top: 1rem; }
  .tech-pill {
    font-family: 'Space Mono', monospace;
    font-size: 0.72rem;
    padding: 6px 14px;
    border-radius: 100px;
    border: 1px solid var(--border);
    color: var(--muted);
    transition: all 0.2s;
  }
  .tech-pill:hover { border-color: var(--green); color: var(--green); }
  .tech-pill.html { border-color: rgba(0,255,157,0.4); color: var(--green); background: rgba(0,255,157,0.06); }

  /* ─── ROLES ─── */
  .roles-grid {
    display: grid; grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
    gap: 1.5rem; margin-top: 3rem;
  }

  .role-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 16px;
    padding: 2rem;
    position: relative; overflow: hidden;
    transition: transform 0.3s, border-color 0.3s, box-shadow 0.3s;
    opacity: 0;
    transform: translateY(30px);
  }
  .role-card.visible { opacity: 1; transform: translateY(0); }
  .role-card:hover { transform: translateY(-6px); box-shadow: 0 20px 60px rgba(0,0,0,0.4); }
  .role-card.admin:hover { border-color: rgba(0,255,157,0.4); box-shadow: 0 20px 60px rgba(0,255,157,0.1); }
  .role-card.manager:hover { border-color: rgba(108,99,255,0.5); box-shadow: 0 20px 60px rgba(108,99,255,0.12); }
  .role-card.employee:hover { border-color: rgba(0,212,255,0.4); box-shadow: 0 20px 60px rgba(0,212,255,0.1); }

  .role-icon {
    width: 52px; height: 52px;
    border-radius: 12px;
    display: flex; align-items: center; justify-content: center;
    font-size: 1.4rem;
    margin-bottom: 1.2rem;
  }
  .admin .role-icon { background: rgba(0,255,157,0.12); }
  .manager .role-icon { background: rgba(108,99,255,0.12); }
  .employee .role-icon { background: rgba(0,212,255,0.12); }
  .receipt-card .role-icon { background: rgba(255,189,0,0.12); }

  .role-name {
    font-size: 1.1rem; font-weight: 700; margin-bottom: 0.5rem;
  }
  .admin .role-name { color: var(--green); }
  .manager .role-name { color: var(--purple); }
  .employee .role-name { color: #00d4ff; }
  .receipt-card .role-name { color: #ffbd00; }

  .role-desc { color: var(--muted); font-size: 0.9rem; line-height: 1.6; margin-bottom: 1.2rem; }

  .feature-list { list-style: none; }
  .feature-list li {
    font-size: 0.85rem; color: #aaa;
    padding: 5px 0;
    display: flex; align-items: center; gap: 8px;
  }
  .feature-list li::before {
    content: '→';
    font-family: 'Space Mono', monospace;
    color: var(--green); font-size: 0.8rem;
    flex-shrink: 0;
  }
  .manager .feature-list li::before { color: var(--purple); }
  .employee .feature-list li::before { color: #00d4ff; }
  .receipt-card .feature-list li::before { color: #ffbd00; }

  /* ─── WORKFLOW ─── */
  #workflow { background: linear-gradient(180deg, var(--darker) 0%, #0a0a14 100%); }

  .flow-steps {
    display: flex; flex-direction: column; gap: 0;
    margin-top: 3rem;
    position: relative;
  }
  .flow-steps::before {
    content: '';
    position: absolute; left: 31px; top: 0; bottom: 0;
    width: 2px;
    background: linear-gradient(to bottom, var(--green), var(--purple), transparent);
  }

  .flow-step {
    display: flex; gap: 2rem; align-items: flex-start;
    padding: 1.5rem 0;
    opacity: 0; transform: translateX(-20px);
    transition: opacity 0.5s, transform 0.5s;
  }
  .flow-step.visible { opacity: 1; transform: translateX(0); }

  .step-num {
    width: 64px; height: 64px; flex-shrink: 0;
    border-radius: 50%;
    background: var(--card);
    border: 2px solid var(--border);
    display: flex; align-items: center; justify-content: center;
    font-family: 'Space Mono', monospace;
    font-size: 1.1rem; font-weight: 700;
    color: var(--green);
    position: relative; z-index: 1;
    transition: border-color 0.3s, box-shadow 0.3s;
  }
  .flow-step:hover .step-num {
    border-color: var(--green);
    box-shadow: 0 0 20px rgba(0,255,157,0.3);
  }

  .step-content h4 {
    font-size: 1.1rem; font-weight: 700; margin-bottom: 0.4rem;
    color: #fff;
  }
  .step-content p { color: var(--muted); font-size: 0.92rem; line-height: 1.6; }

  /* ─── FILES ─── */
  .file-grid {
    display: grid; grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
    gap: 1rem; margin-top: 3rem;
  }

  .file-item {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 1.2rem 1.4rem;
    display: flex; align-items: center; gap: 1rem;
    transition: all 0.25s;
    opacity: 0; transform: scale(0.95);
    cursor: default;
  }
  .file-item.visible { opacity: 1; transform: scale(1); }
  .file-item:hover { border-color: rgba(0,255,157,0.3); background: rgba(0,255,157,0.04); transform: scale(1.02); }

  .file-icon {
    font-size: 1.4rem;
    width: 40px; height: 40px;
    border-radius: 8px;
    background: rgba(0,255,157,0.08);
    display: flex; align-items: center; justify-content: center;
    flex-shrink: 0;
  }

  .file-info small {
    font-family: 'Space Mono', monospace;
    font-size: 0.62rem;
    color: var(--green); letter-spacing: 0.08em;
  }
  .file-info strong { display: block; font-size: 0.88rem; margin-top: 2px; color: var(--text); }

  /* ─── DEPLOY ─── */
  #deploy { background: linear-gradient(135deg, rgba(108,99,255,0.06) 0%, rgba(0,255,157,0.03) 100%); }

  .deploy-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 20px;
    padding: 3rem;
    max-width: 700px; margin: 3rem auto 0;
    text-align: center;
    position: relative; overflow: hidden;
  }
  .deploy-card::before {
    content: '';
    position: absolute; top: 0; left: 0; right: 0;
    height: 3px;
    background: linear-gradient(90deg, var(--green), var(--purple));
  }

  .deploy-url {
    display: inline-flex; align-items: center; gap: 10px;
    font-family: 'Space Mono', monospace;
    font-size: 1rem;
    background: rgba(0,255,157,0.08);
    border: 1px solid rgba(0,255,157,0.2);
    color: var(--green);
    padding: 14px 24px;
    border-radius: 10px;
    margin: 1.5rem 0;
    text-decoration: none;
    transition: all 0.25s;
    word-break: break-all;
  }
  .deploy-url:hover {
    background: rgba(0,255,157,0.15);
    box-shadow: 0 0 30px rgba(0,255,157,0.2);
    transform: scale(1.02);
  }

  .netlify-badge {
    display: inline-flex; align-items: center; gap: 8px;
    font-family: 'Space Mono', monospace;
    font-size: 0.72rem;
    color: var(--muted);
    margin-top: 1rem;
    padding: 8px 16px;
    border: 1px solid var(--border);
    border-radius: 100px;
  }

  /* ─── FOOTER ─── */
  footer {
    position: relative; z-index: 1;
    border-top: 1px solid var(--border);
    padding: 2.5rem 2rem;
    text-align: center;
  }
  .footer-text {
    font-family: 'Space Mono', monospace;
    font-size: 0.75rem;
    color: var(--muted);
    letter-spacing: 0.08em;
  }
  .footer-text span { color: var(--green); }

  /* ─── ANIMATIONS ─── */
  @keyframes fadeSlideDown {
    from { opacity: 0; transform: translateY(-20px); }
    to { opacity: 1; transform: translateY(0); }
  }
  @keyframes fadeSlideUp {
    from { opacity: 0; transform: translateY(30px); }
    to { opacity: 1; transform: translateY(0); }
  }

  /* ─── RESPONSIVE ─── */
  @media (max-width: 768px) {
    .about-grid { grid-template-columns: 1fr; gap: 2rem; }
    .flow-steps::before { left: 23px; }
    .step-num { width: 48px; height: 48px; font-size: 0.9rem; }
    .deploy-card { padding: 2rem 1.5rem; }
  }
</style>
</head>
<body>

<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursorRing"></div>

<canvas id="particles"></canvas>

<!-- ─── HERO ─── -->
<section class="hero">
  <div class="hero-glow"></div>

  <div class="badge">
    <span class="badge-dot"></span>
    HACKATHON PROJECT · CE EDITION
  </div>

  <h1 class="hero-title">
    <span class="line1">EXPENSE</span>
    <span class="line2">APPROVALS</span>
  </h1>

  <p class="hero-sub">
    A role-based expense management system with smart approval workflows, sequential routing, and multi-tier access control — built in pure HTML &amp; CSS.
  </p>

  <div class="hero-btns">
    <a href="https://ce-hackathon.netlify.app/" target="_blank" class="btn btn-primary">
      🚀 Live Demo
    </a>
    <a href="https://github.com/DhruvOzha85/CE-HACKATHON" target="_blank" class="btn btn-outline">
      ⌥ View Source
    </a>
  </div>

  <div class="stats-strip">
    <div class="stat">
      <div class="stat-num">6</div>
      <div class="stat-label">HTML Pages</div>
    </div>
    <div class="stat-divider"></div>
    <div class="stat">
      <div class="stat-num">4</div>
      <div class="stat-label">User Roles</div>
    </div>
    <div class="stat-divider"></div>
    <div class="stat">
      <div class="stat-num">100%</div>
      <div class="stat-label">Frontend</div>
    </div>
    <div class="stat-divider"></div>
    <div class="stat">
      <div class="stat-num">∞</div>
      <div class="stat-label">Scalable Rules</div>
    </div>
  </div>

  <div class="scroll-hint">
    <span>SCROLL</span>
    <div class="scroll-line"></div>
  </div>
</section>

<div class="divider"></div>

<!-- ─── ABOUT ─── -->
<section id="about">
  <div class="container">
    <div class="section-label">// 01 — OVERVIEW</div>
    <h2 class="section-title">What is CE-HACKATHON?</h2>

    <div class="about-grid">
      <div class="about-text">
        <p>
          CE-HACKATHON is a <span>Corporate Expense Approval System</span> built for a hackathon challenge. It implements a complete end-to-end approval workflow for employee expense requests.
        </p>
        <p>
          The platform supports <span>sequential and parallel approval routing</span>, required approver enforcement, configurable minimum-approval thresholds, and manager-first escalation — all managed through an intuitive dark-themed UI.
        </p>
        <p>
          Every role gets a <span>dedicated view</span>: Admins configure rules, Managers approve or reject, Employees submit requests, and Receipts are tracked across the lifecycle.
        </p>
      </div>

      <div class="about-card">
        <div class="section-label" style="margin-bottom:1rem;">TECH STACK</div>
        <div class="tech-stack">
          <span class="tech-pill html">HTML5</span>
          <span class="tech-pill html">CSS3</span>
          <span class="tech-pill html">Vanilla JS</span>
          <span class="tech-pill">Netlify</span>
          <span class="tech-pill">Font Awesome</span>
          <span class="tech-pill">CSS Animations</span>
          <span class="tech-pill">CSS Variables</span>
          <span class="tech-pill">Flexbox</span>
          <span class="tech-pill">CSS Grid</span>
        </div>

        <div style="margin-top:2rem;">
          <div class="section-label" style="margin-bottom:0.8rem;">DEPLOYMENT</div>
          <div style="display:flex;align-items:center;gap:10px;color:var(--green);font-family:'Space Mono',monospace;font-size:0.82rem;">
            <span>⚡</span> Netlify CDN — Instant Deploy
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<div class="divider"></div>

<!-- ─── ROLES ─── -->
<section id="roles">
  <div class="container">
    <div class="section-label">// 02 — ROLE-BASED VIEWS</div>
    <h2 class="section-title">Four Roles, One System</h2>

    <div class="roles-grid">
      <!-- Admin -->
      <div class="role-card admin">
        <div class="role-icon">🛡️</div>
        <div class="role-name">Admin</div>
        <p class="role-desc">Configures the approval framework for the entire organization. Sets rules, assigns approvers, and defines thresholds.</p>
        <ul class="feature-list">
          <li>Define approval rules per user</li>
          <li>Assign required approvers</li>
          <li>Toggle sequential vs parallel flow</li>
          <li>Set manager-first escalation</li>
          <li>Configure min. approval percentage</li>
        </ul>
      </div>

      <!-- Manager -->
      <div class="role-card manager">
        <div class="role-icon">👔</div>
        <div class="role-name">Manager</div>
        <p class="role-desc">Reviews pending expense requests from team members. Can approve or reject based on policy and budget.</p>
        <ul class="feature-list">
          <li>View pending requests</li>
          <li>Approve or reject expenses</li>
          <li>Add comments/remarks</li>
          <li>Track approval history</li>
          <li>Receive first-pass escalations</li>
        </ul>
      </div>

      <!-- Employee -->
      <div class="role-card employee">
        <div class="role-icon">👤</div>
        <div class="role-name">Employee</div>
        <p class="role-desc">Submits expense claims and tracks their approval status through the workflow in real time.</p>
        <ul class="feature-list">
          <li>Submit new expense requests</li>
          <li>Track request status</li>
          <li>View approval chain progress</li>
          <li>Receive auto-rejection alerts</li>
          <li>Access past submissions</li>
        </ul>
      </div>

      <!-- Receipt -->
      <div class="role-card receipt-card">
        <div class="role-icon">🧾</div>
        <div class="role-name">Receipt</div>
        <p class="role-desc">Generates and displays a structured receipt upon final approval, creating an audit-ready record of every transaction.</p>
        <ul class="feature-list">
          <li>Auto-generated on approval</li>
          <li>Full audit trail</li>
          <li>Expense summary breakdown</li>
          <li>Approval chain record</li>
        </ul>
      </div>
    </div>
  </div>
</section>

<div class="divider"></div>

<!-- ─── WORKFLOW ─── -->
<section id="workflow">
  <div class="container">
    <div class="section-label">// 03 — APPROVAL WORKFLOW</div>
    <h2 class="section-title">How It Works</h2>

    <div class="flow-steps">
      <div class="flow-step">
        <div class="step-num">01</div>
        <div class="step-content">
          <h4>Employee Submits Expense</h4>
          <p>An employee logs in and files a new expense request via the Employee View. They add description, amount, and supporting details.</p>
        </div>
      </div>
      <div class="flow-step">
        <div class="step-num">02</div>
        <div class="step-content">
          <h4>Manager Gets First Look</h4>
          <p>If admin has enabled "Manager is Approver", the request is automatically routed to the employee's direct manager first.</p>
        </div>
      </div>
      <div class="flow-step">
        <div class="step-num">03</div>
        <div class="step-content">
          <h4>Sequential or Parallel Routing</h4>
          <p>The admin-configured approver sequence kicks in. Requests can go to all approvers simultaneously or one-by-one in order — your choice.</p>
        </div>
      </div>
      <div class="flow-step">
        <div class="step-num">04</div>
        <div class="step-content">
          <h4>Required Approvers Must Sign Off</h4>
          <p>Any approver marked "Required" must explicitly approve. If a required approver rejects, the expense is auto-rejected immediately.</p>
        </div>
      </div>
      <div class="flow-step">
        <div class="step-num">05</div>
        <div class="step-content">
          <h4>Threshold Check</h4>
          <p>After all approvers vote, the system checks if the minimum approval percentage (e.g., 60%) has been met. Only then is the expense approved.</p>
        </div>
      </div>
      <div class="flow-step">
        <div class="step-num">06</div>
        <div class="step-content">
          <h4>Receipt Generated</h4>
          <p>On final approval, a formal receipt is generated with the full expense record and approval chain — ready for accounting.</p>
        </div>
      </div>
    </div>
  </div>
</section>

<div class="divider"></div>

<!-- ─── FILE STRUCTURE ─── -->
<section id="files">
  <div class="container">
    <div class="section-label">// 04 — FILE STRUCTURE</div>
    <h2 class="section-title">Project Files</h2>

    <div class="file-grid">
      <div class="file-item">
        <div class="file-icon">🔐</div>
        <div class="file-info">
          <small>ENTRY POINT</small>
          <strong>SignUp_Login_Page.html</strong>
        </div>
      </div>
      <div class="file-item">
        <div class="file-icon">🛡️</div>
        <div class="file-info">
          <small>ADMIN</small>
          <strong>AdminView.html</strong>
        </div>
      </div>
      <div class="file-item">
        <div class="file-icon">👔</div>
        <div class="file-info">
          <small>MANAGER</small>
          <strong>managerview.html</strong>
        </div>
      </div>
      <div class="file-item">
        <div class="file-icon">👤</div>
        <div class="file-info">
          <small>EMPLOYEE</small>
          <strong>employeeView.html</strong>
        </div>
      </div>
      <div class="file-item">
        <div class="file-icon">⚙️</div>
        <div class="file-info">
          <small>ROLE MGMT</small>
          <strong>UserRoleManager.html</strong>
        </div>
      </div>
      <div class="file-item">
        <div class="file-icon">🧾</div>
        <div class="file-info">
          <small>RECEIPT</small>
          <strong>receipt.html</strong>
        </div>
      </div>
    </div>
  </div>
</section>

<div class="divider"></div>

<!-- ─── DEPLOYMENT ─── -->
<section id="deploy">
  <div class="container">
    <div class="section-label">// 05 — DEPLOYMENT</div>
    <h2 class="section-title">Live &amp; Ready</h2>

    <div class="deploy-card">
      <p style="color:var(--muted);font-size:0.95rem;line-height:1.7;">
        The project is deployed and live on Netlify. No backend required — pure client-side experience.
      </p>

      <a href="https://ce-hackathon.netlify.app/" target="_blank" class="deploy-url">
        🌐 &nbsp;ce-hackathon.netlify.app
      </a>

      <div style="display:flex;justify-content:center;gap:1rem;flex-wrap:wrap;margin-top:1.5rem;">
        <div class="netlify-badge">⚡ Netlify CDN</div>
        <div class="netlify-badge">🔒 HTTPS Enabled</div>
        <div class="netlify-badge">📦 Static Hosting</div>
      </div>

      <div style="margin-top:2.5rem;padding-top:2rem;border-top:1px solid var(--border);">
        <p style="font-family:'Space Mono',monospace;font-size:0.75rem;color:var(--muted);margin-bottom:1rem;">CLONE &amp; RUN LOCALLY</p>
        <div style="background:#0a0a0a;border:1px solid var(--border);border-radius:10px;padding:1.2rem;text-align:left;font-family:'Space Mono',monospace;font-size:0.8rem;color:var(--green);line-height:2;">
          <span style="color:var(--muted);"># clone the repo</span><br>
          git clone https://github.com/DhruvOzha85/CE-HACKATHON<br>
          <span style="color:var(--muted);"># open in browser</span><br>
          open SignUp_Login_Page.html
        </div>
      </div>
    </div>
  </div>
</section>

<!-- ─── FOOTER ─── -->
<footer>
  <p class="footer-text">
    Built with <span>♥</span> for the CE Hackathon &nbsp;·&nbsp;
    <span>DhruvOzha85</span> &nbsp;·&nbsp;
    Deployed on <span>Netlify</span>
  </p>
</footer>

<script>
  // ── Custom cursor
  const cursor = document.getElementById('cursor');
  const ring = document.getElementById('cursorRing');
  let mx = 0, my = 0, rx = 0, ry = 0;
  document.addEventListener('mousemove', e => { mx = e.clientX; my = e.clientY; });
  function animCursor() {
    cursor.style.left = mx + 'px'; cursor.style.top = my + 'px';
    rx += (mx - rx) * 0.12; ry += (my - ry) * 0.12;
    ring.style.left = rx + 'px'; ring.style.top = ry + 'px';
    requestAnimationFrame(animCursor);
  }
  animCursor();

  // ── Particle canvas
  const canvas = document.getElementById('particles');
  const ctx = canvas.getContext('2d');
  let W, H, dots = [];
  function resize() { W = canvas.width = innerWidth; H = canvas.height = innerHeight; }
  resize(); window.addEventListener('resize', resize);

  for (let i = 0; i < 80; i++) dots.push({
    x: Math.random() * 2000, y: Math.random() * 2000,
    vx: (Math.random() - 0.5) * 0.3, vy: (Math.random() - 0.5) * 0.3,
    r: Math.random() * 1.5 + 0.5,
    color: Math.random() > 0.5 ? '#00ff9d' : '#6c63ff'
  });

  function drawParticles() {
    ctx.clearRect(0,0,W,H);
    dots.forEach(d => {
      d.x += d.vx; d.y += d.vy;
      if (d.x < 0) d.x = W; if (d.x > W) d.x = 0;
      if (d.y < 0) d.y = H; if (d.y > H) d.y = 0;
      ctx.beginPath();
      ctx.arc(d.x, d.y, d.r, 0, Math.PI*2);
      ctx.fillStyle = d.color + '55';
      ctx.fill();
    });
    // draw connections
    for (let i = 0; i < dots.length; i++) {
      for (let j = i+1; j < dots.length; j++) {
        const dx = dots[i].x - dots[j].x, dy = dots[i].y - dots[j].y;
        const dist = Math.sqrt(dx*dx + dy*dy);
        if (dist < 120) {
          ctx.beginPath();
          ctx.moveTo(dots[i].x, dots[i].y);
          ctx.lineTo(dots[j].x, dots[j].y);
          ctx.strokeStyle = `rgba(108,99,255,${(1 - dist/120) * 0.15})`;
          ctx.lineWidth = 0.5;
          ctx.stroke();
        }
      }
    }
    requestAnimationFrame(drawParticles);
  }
  drawParticles();

  // ── Scroll animations
  const observer = new IntersectionObserver((entries) => {
    entries.forEach((e, i) => {
      if (e.isIntersecting) {
        setTimeout(() => e.target.classList.add('visible'), e.target.dataset.delay || 0);
      }
    });
  }, { threshold: 0.15 });

  document.querySelectorAll('.role-card').forEach((el, i) => {
    el.dataset.delay = i * 100;
    observer.observe(el);
  });
  document.querySelectorAll('.flow-step').forEach((el, i) => {
    el.dataset.delay = i * 120;
    observer.observe(el);
  });
  document.querySelectorAll('.file-item').forEach((el, i) => {
    el.dataset.delay = i * 80;
    observer.observe(el);
  });

  // ── Smooth role card transition
  document.querySelectorAll('.role-card').forEach(card => {
    card.style.transition = 'opacity 0.5s ease, transform 0.5s ease, border-color 0.3s, box-shadow 0.3s';
  });
</script>
</body>
</html>
