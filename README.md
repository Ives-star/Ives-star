<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>BCP Toolkit — Interactive Study Guide</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=DM+Sans:ital,wght@0,300;0,400;0,500;1,300&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #0d1117;
    --surface: #161b22;
    --card: #1c2330;
    --border: #30363d;
    --accent: #f0a500;
    --accent2: #e05a2b;
    --accent3: #2db36b;
    --text: #e6edf3;
    --muted: #8b949e;
    --danger: #f85149;
    --success: #3fb950;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'DM Sans', sans-serif;
    min-height: 100vh;
    overflow-x: hidden;
  }

  /* ── HEADER ── */
  header {
    padding: 3rem 2rem 2rem;
    background: linear-gradient(135deg, #0d1117 0%, #1a1f2e 60%, #0d1117 100%);
    border-bottom: 1px solid var(--border);
    text-align: center;
    position: relative;
    overflow: hidden;
  }
  header::before {
    content: '';
    position: absolute;
    inset: 0;
    background: radial-gradient(ellipse at 50% -20%, rgba(240,165,0,0.15) 0%, transparent 60%);
    pointer-events: none;
  }
  header .tag {
    display: inline-block;
    background: rgba(240,165,0,0.15);
    border: 1px solid var(--accent);
    color: var(--accent);
    font-size: 0.7rem;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    padding: 0.3rem 0.9rem;
    border-radius: 100px;
    margin-bottom: 1rem;
    font-family: 'Syne', sans-serif;
    font-weight: 600;
  }
  header h1 {
    font-family: 'Syne', sans-serif;
    font-weight: 800;
    font-size: clamp(1.8rem, 5vw, 3rem);
    line-height: 1.1;
    letter-spacing: -0.02em;
  }
  header h1 span { color: var(--accent); }
  header p.sub {
    margin-top: 0.8rem;
    color: var(--muted);
    font-size: 0.95rem;
    font-weight: 300;
  }

  /* ── NAV ── */
  nav {
    display: flex;
    gap: 0.5rem;
    justify-content: center;
    flex-wrap: wrap;
    padding: 1.2rem 1rem;
    background: var(--surface);
    border-bottom: 1px solid var(--border);
    position: sticky;
    top: 0;
    z-index: 100;
  }
  nav button {
    background: transparent;
    border: 1px solid var(--border);
    color: var(--muted);
    padding: 0.45rem 1.1rem;
    border-radius: 100px;
    font-family: 'DM Sans', sans-serif;
    font-size: 0.82rem;
    cursor: pointer;
    transition: all 0.2s;
    letter-spacing: 0.02em;
  }
  nav button:hover { border-color: var(--accent); color: var(--accent); }
  nav button.active {
    background: var(--accent);
    border-color: var(--accent);
    color: #000;
    font-weight: 600;
  }

  /* ── SECTIONS ── */
  .section { display: none; padding: 2rem; max-width: 900px; margin: 0 auto; }
  .section.active { display: block; }

  /* ── SECTION TITLE ── */
  .sec-title {
    font-family: 'Syne', sans-serif;
    font-size: 1.5rem;
    font-weight: 700;
    margin-bottom: 1.5rem;
    display: flex;
    align-items: center;
    gap: 0.7rem;
  }
  .sec-title .icon {
    width: 36px; height: 36px;
    background: var(--accent);
    border-radius: 8px;
    display: flex; align-items: center; justify-content: center;
    font-size: 1rem;
    flex-shrink: 0;
  }

  /* ── CARDS ── */
  .card-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
    gap: 1rem;
    margin-bottom: 2rem;
  }
  .card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 1.4rem;
    transition: border-color 0.2s, transform 0.2s;
  }
  .card:hover { border-color: var(--accent); transform: translateY(-2px); }
  .card h3 {
    font-family: 'Syne', sans-serif;
    font-size: 0.95rem;
    font-weight: 700;
    margin-bottom: 0.6rem;
    color: var(--accent);
  }
  .card p { font-size: 0.88rem; color: var(--muted); line-height: 1.6; }
  .card .badge {
    display: inline-block;
    font-size: 0.68rem;
    padding: 0.2rem 0.6rem;
    border-radius: 100px;
    margin-bottom: 0.7rem;
    font-weight: 600;
    letter-spacing: 0.05em;
    text-transform: uppercase;
  }
  .badge-red { background: rgba(248,81,73,0.15); color: var(--danger); border: 1px solid rgba(248,81,73,0.3); }
  .badge-green { background: rgba(63,185,80,0.15); color: var(--success); border: 1px solid rgba(63,185,80,0.3); }
  .badge-orange { background: rgba(240,165,0,0.15); color: var(--accent); border: 1px solid rgba(240,165,0,0.3); }
  .badge-blue { background: rgba(88,166,255,0.15); color: #58a6ff; border: 1px solid rgba(88,166,255,0.3); }

  /* ── STEPS ── */
  .steps { display: flex; flex-direction: column; gap: 0; margin-bottom: 2rem; }
  .step {
    display: flex;
    gap: 1rem;
    position: relative;
    padding-bottom: 1.5rem;
  }
  .step:last-child { padding-bottom: 0; }
  .step-num {
    width: 36px; height: 36px;
    background: var(--accent);
    color: #000;
    border-radius: 50%;
    display: flex; align-items: center; justify-content: center;
    font-family: 'Syne', sans-serif;
    font-weight: 800;
    font-size: 0.85rem;
    flex-shrink: 0;
    position: relative;
    z-index: 1;
  }
  .step-line {
    position: absolute;
    left: 17px; top: 36px; bottom: 0;
    width: 2px;
    background: var(--border);
  }
  .step:last-child .step-line { display: none; }
  .step-content {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 1rem 1.2rem;
    flex: 1;
  }
  .step-content h4 { font-family: 'Syne', sans-serif; font-size: 0.9rem; font-weight: 700; margin-bottom: 0.4rem; }
  .step-content p { font-size: 0.83rem; color: var(--muted); line-height: 1.6; }

  /* ── QUIZ ── */
  .quiz-container { max-width: 700px; }
  .quiz-progress {
    display: flex;
    gap: 0.3rem;
    margin-bottom: 1.5rem;
  }
  .quiz-dot {
    height: 4px;
    flex: 1;
    border-radius: 100px;
    background: var(--border);
    transition: background 0.3s;
  }
  .quiz-dot.done { background: var(--accent); }
  .quiz-dot.correct { background: var(--success); }
  .quiz-dot.wrong { background: var(--danger); }
  .question-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 14px;
    padding: 1.8rem;
    margin-bottom: 1rem;
  }
  .question-card .q-num {
    font-size: 0.75rem;
    color: var(--muted);
    font-weight: 500;
    margin-bottom: 0.5rem;
    letter-spacing: 0.1em;
    text-transform: uppercase;
  }
  .question-card h3 {
    font-family: 'Syne', sans-serif;
    font-size: 1.05rem;
    font-weight: 700;
    line-height: 1.5;
    margin-bottom: 1.2rem;
  }
  .options { display: flex; flex-direction: column; gap: 0.6rem; }
  .option {
    background: var(--surface);
    border: 1.5px solid var(--border);
    border-radius: 10px;
    padding: 0.85rem 1.1rem;
    cursor: pointer;
    font-size: 0.88rem;
    transition: all 0.2s;
    text-align: left;
    color: var(--text);
    font-family: 'DM Sans', sans-serif;
    line-height: 1.5;
  }
  .option:hover:not(:disabled) { border-color: var(--accent); background: rgba(240,165,0,0.05); }
  .option.correct { border-color: var(--success); background: rgba(63,185,80,0.1); color: var(--success); }
  .option.wrong { border-color: var(--danger); background: rgba(248,81,73,0.1); color: var(--danger); }
  .option:disabled { cursor: not-allowed; }
  .feedback {
    padding: 0.8rem 1rem;
    border-radius: 8px;
    font-size: 0.85rem;
    margin-top: 0.8rem;
    display: none;
    line-height: 1.5;
  }
  .feedback.show { display: block; }
  .feedback.correct { background: rgba(63,185,80,0.1); border: 1px solid rgba(63,185,80,0.3); color: var(--success); }
  .feedback.wrong { background: rgba(248,81,73,0.1); border: 1px solid rgba(248,81,73,0.3); color: var(--danger); }
  .quiz-nav {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-top: 1rem;
  }
  .btn {
    background: var(--accent);
    color: #000;
    border: none;
    padding: 0.65rem 1.5rem;
    border-radius: 8px;
    font-family: 'Syne', sans-serif;
    font-weight: 700;
    font-size: 0.85rem;
    cursor: pointer;
    transition: opacity 0.2s;
    letter-spacing: 0.03em;
  }
  .btn:hover { opacity: 0.85; }
  .btn:disabled { opacity: 0.3; cursor: not-allowed; }
  .btn-ghost {
    background: transparent;
    border: 1.5px solid var(--border);
    color: var(--muted);
  }
  .btn-ghost:hover { border-color: var(--accent); color: var(--accent); }
  .score-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 14px;
    padding: 2.5rem;
    text-align: center;
  }
  .score-num {
    font-family: 'Syne', sans-serif;
    font-size: 3.5rem;
    font-weight: 800;
    color: var(--accent);
    line-height: 1;
  }
  .score-label { color: var(--muted); margin-top: 0.3rem; font-size: 0.9rem; }

  /* ── FLASHCARDS ── */
  .flashcard-wrap {
    perspective: 1000px;
    width: 100%;
    max-width: 560px;
    margin: 0 auto 1.5rem;
    cursor: pointer;
  }
  .flashcard {
    width: 100%;
    height: 200px;
    position: relative;
    transform-style: preserve-3d;
    transition: transform 0.5s ease;
  }
  .flashcard.flipped { transform: rotateY(180deg); }
  .fc-face {
    position: absolute;
    inset: 0;
    background: var(--card);
    border: 1.5px solid var(--border);
    border-radius: 16px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 1.5rem;
    backface-visibility: hidden;
    -webkit-backface-visibility: hidden;
    text-align: center;
  }
  .fc-back { transform: rotateY(180deg); }
  .fc-face .fc-label {
    font-size: 0.68rem;
    text-transform: uppercase;
    letter-spacing: 0.12em;
    color: var(--muted);
    margin-bottom: 0.8rem;
    font-weight: 600;
  }
  .fc-face h3 {
    font-family: 'Syne', sans-serif;
    font-size: 1.1rem;
    font-weight: 700;
    line-height: 1.4;
  }
  .fc-face p { font-size: 0.85rem; color: var(--muted); line-height: 1.6; }
  .fc-hint { font-size: 0.72rem; color: var(--muted); margin-top: 0.5rem; }
  .fc-nav {
    display: flex;
    gap: 1rem;
    justify-content: center;
    align-items: center;
  }
  .fc-counter { font-size: 0.82rem; color: var(--muted); }

  /* ── CHECKLIST ── */
  .checklist-item {
    display: flex;
    gap: 1rem;
    align-items: flex-start;
    padding: 0.9rem 1rem;
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 10px;
    margin-bottom: 0.6rem;
    cursor: pointer;
    transition: border-color 0.2s;
  }
  .checklist-item:hover { border-color: var(--accent); }
  .checklist-item.checked { border-color: var(--success); background: rgba(63,185,80,0.05); }
  .check-box {
    width: 20px; height: 20px;
    border: 2px solid var(--border);
    border-radius: 5px;
    flex-shrink: 0;
    margin-top: 2px;
    display: flex; align-items: center; justify-content: center;
    transition: all 0.2s;
  }
  .checklist-item.checked .check-box {
    background: var(--success);
    border-color: var(--success);
    color: #fff;
    font-size: 12px;
  }
  .check-text { font-size: 0.88rem; line-height: 1.5; }
  .check-text.checked { text-decoration: line-through; color: var(--muted); }
  .progress-bar-wrap { background: var(--surface); border-radius: 100px; height: 6px; margin-bottom: 1.5rem; overflow: hidden; }
  .progress-bar-fill { height: 100%; background: var(--success); border-radius: 100px; transition: width 0.4s; }

  /* ── ACCORDION ── */
  .accordion { margin-bottom: 0.6rem; }
  .acc-header {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 1rem 1.2rem;
    cursor: pointer;
    display: flex;
    justify-content: space-between;
    align-items: center;
    transition: border-color 0.2s;
  }
  .acc-header:hover { border-color: var(--accent); }
  .acc-header.open { border-color: var(--accent); border-bottom-left-radius: 0; border-bottom-right-radius: 0; }
  .acc-header h4 { font-family: 'Syne', sans-serif; font-size: 0.9rem; font-weight: 700; }
  .acc-arrow { color: var(--muted); transition: transform 0.2s; font-size: 0.9rem; }
  .acc-header.open .acc-arrow { transform: rotate(180deg); }
  .acc-body {
    display: none;
    background: rgba(28,35,48,0.5);
    border: 1px solid var(--accent);
    border-top: none;
    border-bottom-left-radius: 10px;
    border-bottom-right-radius: 10px;
    padding: 1rem 1.2rem;
    font-size: 0.85rem;
    color: var(--muted);
    line-height: 1.7;
  }
  .acc-body.open { display: block; }
  .acc-body ul { padding-left: 1.2rem; }
  .acc-body ul li { margin-bottom: 0.4rem; }

  /* ── TAGS ── */
  .tag-row { display: flex; flex-wrap: wrap; gap: 0.5rem; margin-bottom: 1.5rem; }
  .tag-chip {
    background: var(--surface);
    border: 1px solid var(--border);
    padding: 0.3rem 0.8rem;
    border-radius: 100px;
    font-size: 0.78rem;
    color: var(--muted);
  }
  .tag-chip.hi { border-color: var(--danger); color: var(--danger); background: rgba(248,81,73,0.08); }
  .tag-chip.med { border-color: var(--accent); color: var(--accent); background: rgba(240,165,0,0.08); }
  .tag-chip.lo { border-color: var(--success); color: var(--success); background: rgba(63,185,80,0.08); }

  @media(max-width:500px) {
    .section { padding: 1rem; }
    header { padding: 2rem 1rem 1.5rem; }
  }
</style>
</head>
<body>

<header>
  <div class="tag">Caribbean Development Bank · 2023</div>
  <h1>Business Continuity<br><span>Planning Toolkit</span></h1>
  <p class="sub">Interactive study guide for Micro, Small & Medium Enterprises</p>
</header>

<nav>
  <button class="active" onclick="show('overview')">📋 Overview</button>
  <button onclick="show('hazards')">⚠️ Hazards</button>
  <button onclick="show('planning')">🗂 Planning</button>
  <button onclick="show('financial')">💰 Financial</button>
  <button onclick="show('flashcards')">🃏 Flashcards</button>
  <button onclick="show('quiz')">🧠 Quiz</button>
  <button onclick="show('checklist')">✅ Checklist</button>
</nav>

<!-- ══ OVERVIEW ══ -->
<section id="overview" class="section active">
  <div class="sec-title"><span class="icon">📋</span> Toolkit Overview</div>

  <div class="card-grid">
    <div class="card">
      <div class="badge badge-blue">Section 1</div>
      <h3>Context & Hazards</h3>
      <p>Overview of Caribbean MSME constraints (operational, economic, social, technology) and natural & man-made hazards affecting the region.</p>
    </div>
    <div class="card">
      <div class="badge badge-orange">Section 2</div>
      <h3>Data Collection & Analysis</h3>
      <p>Checklists and tables to gather info for your BCP — hazard/vulnerability analysis, business impact analysis, and resource identification.</p>
    </div>
    <div class="card">
      <div class="badge badge-green">Section 3</div>
      <h3>Plan Template</h3>
      <p>A ready-to-fill template where you put all analysis results to produce your actual Business Continuity Plan.</p>
    </div>
    <div class="card">
      <div class="badge badge-red">Section 4</div>
      <h3>Mini Case Studies</h3>
      <p>Real-world Caribbean disaster scenarios to help you think through how different events affect businesses.</p>
    </div>
  </div>

  <div class="sec-title" style="font-size:1.1rem; margin-top:1rem;"><span>🏢</span> MSME Size Definitions (CDB)</div>
  <div class="card-grid">
    <div class="card"><h3>Micro Enterprise</h3><p>5 or fewer employees</p></div>
    <div class="card"><h3>Small Enterprise</h3><p>6 to 15 employees</p></div>
    <div class="card"><h3>Medium Enterprise</h3><p>16 to 59 employees</p></div>
  </div>

  <div class="sec-title" style="font-size:1.1rem;"><span>🎯</span> Why Plan?</div>
  <div class="accordion">
    <div class="acc-header" onclick="toggleAcc(this)"><h4>Reduces chaos after a disaster</h4><span class="acc-arrow">▼</span></div>
    <div class="acc-body">A plan minimizes the thinking time required after an event. What would otherwise be arbitrary and chaotic becomes systematic and orderly.</div>
  </div>
  <div class="accordion">
    <div class="acc-header" onclick="toggleAcc(this)"><h4>Everyone knows their role</h4><span class="acc-arrow">▼</span></div>
    <div class="acc-body">A BCP ensures all staff understand what they are required to do before, during, and after a disaster — preventing confusion and wasted time.</div>
  </div>
  <div class="accordion">
    <div class="acc-header" onclick="toggleAcc(this)"><h4>Faster business resumption</h4><span class="acc-arrow">▼</span></div>
    <div class="acc-body">By preparing in advance, the business can continue or restart operations quickly, protecting revenue and customer relationships.</div>
  </div>
  <div class="accordion">
    <div class="acc-header" onclick="toggleAcc(this)"><h4>Protects life, property & operations</h4><span class="acc-arrow">▼</span></div>
    <div class="acc-body">The ultimate aim is to reduce loss of life and property, ensure effective resource mobilization, and promote speedy recovery.</div>
  </div>
</section>

<!-- ══ HAZARDS ══ -->
<section id="hazards" class="section">
  <div class="sec-title"><span class="icon">⚠️</span> Hazards in the Caribbean</div>

  <div class="card-grid">
    <div class="card">
      <div class="badge badge-red">High Risk</div>
      <h3>🌀 Hurricanes</h3>
      <p>At least one major Category 3+ hurricane crosses the Caribbean yearly. In 2017, Hurricanes Irma & Maria caused USD $3.3 billion in damage to 4 CDB member countries. Losses can exceed a country's entire annual GDP.</p>
    </div>
    <div class="card">
      <div class="badge badge-red">High Risk</div>
      <h3>🌊 Floods</h3>
      <p>Coastal flooding from storm surges, and inland flooding from intense rainfall. Often associated with tropical storms and hurricanes.</p>
    </div>
    <div class="card">
      <div class="badge badge-orange">Moderate Risk</div>
      <h3>🌋 Volcanoes & Earthquakes</h3>
      <p>Active volcanoes include Soufrière Hills (Montserrat) and La Soufrière (St. Vincent). The 2021 SVG eruption destroyed up to 50% of GDP. Earthquakes ranging 2–8 on the Richter scale are common.</p>
    </div>
    <div class="card">
      <div class="badge badge-orange">Moderate Risk</div>
      <h3>🪨 Landslides</h3>
      <p>Most common natural hazard in Jamaica. Triggered by heavy rains; steep topography in Dominica and the Northern Range (Trinidad) is especially prone.</p>
    </div>
    <div class="card">
      <div class="badge badge-orange">Moderate Risk</div>
      <h3>☀️ Drought</h3>
      <p>7 Caribbean countries are among the world's top 36 most water-stressed. Barbados, Antigua & Barbuda, and St. Kitts & Nevis are classified as water-scarce.</p>
    </div>
    <div class="card">
      <div class="badge badge-red">High Risk</div>
      <h3>🧪 Epidemics / Pandemics</h3>
      <p>COVID-19, Dengue, Chikungunya, ZIKA, Bird Flu, and Foot and Mouth disease all represent biological hazards that can disrupt business operations.</p>
    </div>
    <div class="card">
      <div class="badge badge-blue">Man-Made</div>
      <h3>🔥 Fires</h3>
      <p>Domestic and forest fires. Forest fires associated with dry seasons in Trinidad, Jamaica, Belize & Guyana. Domestic fires can destroy home-based businesses.</p>
    </div>
    <div class="card">
      <div class="badge badge-blue">Man-Made</div>
      <h3>⚗️ Technological Hazards</h3>
      <p>Oil spills (on-shore and off-shore), nuclear waste transport, hazardous chemical storage, and toxic releases pose threats to Caribbean businesses.</p>
    </div>
  </div>

  <div class="sec-title" style="font-size:1.1rem; margin-top:1rem;"><span>🏗</span> MSME Constraints</div>
  <div class="card-grid">
    <div class="card"><div class="badge badge-orange">Operational</div><h3>Equipment & Personnel</h3><p>Limited access to equipment, lack of trained staff, certification barriers, location vulnerability, rising energy costs, limited ICT access.</p></div>
    <div class="card"><div class="badge badge-red">Economic</div><h3>Finance & Trade</h3><p>Prohibitive lending/tax rates, global market trends, erosion of trade preferences, high transport costs, inadequate broadband.</p></div>
    <div class="card"><div class="badge badge-blue">Social</div><h3>Community Challenges</h3><p>Poverty, illiteracy, poor education, limited healthcare access, crime — all compounding business fragility.</p></div>
    <div class="card"><div class="badge badge-green">Gender</div><h3>Women in MSMEs</h3><p>Women face more financing restrictions and are often excluded from digital training. Greater unpaid care burdens limit time for innovation.</p></div>
  </div>
</section>

<!-- ══ PLANNING ══ -->
<section id="planning" class="section">
  <div class="sec-title"><span class="icon">🗂</span> The Planning Process</div>

  <p style="color:var(--muted); font-size:0.88rem; margin-bottom:1.5rem;">Follow these 10 steps to build a complete Business Continuity Plan.</p>

  <div class="steps">
    <div class="step">
      <div class="step-num">1</div>
      <div class="step-line"></div>
      <div class="step-content"><h4>Identify plan author & responsibilities</h4><p>Who will write and own the plan? Assign a BCP team leader.</p></div>
    </div>
    <div class="step">
      <div class="step-num">2</div>
      <div class="step-line"></div>
      <div class="step-content"><h4>Define activation & deactivation triggers</h4><p>When does the plan kick in? What conditions signal it can be stood down?</p></div>
    </div>
    <div class="step">
      <div class="step-num">3</div>
      <div class="step-line"></div>
      <div class="step-content"><h4>Establish communication methods</h4><p>How will staff, customers, and suppliers be contacted when normal channels fail?</p></div>
    </div>
    <div class="step">
      <div class="step-num">4</div>
      <div class="step-line"></div>
      <div class="step-content"><h4>Conduct Site Vulnerability Analysis</h4><p>Assess storm surge, flooding, earthquake, drought and hazardous materials risk at your location.</p></div>
    </div>
    <div class="step">
      <div class="step-num">5</div>
      <div class="step-line"></div>
      <div class="step-content"><h4>Perform Business Impact Analysis (BIA)</h4><p>Identify critical functions, prioritize by impact level, and determine maximum tolerable downtime for each.</p></div>
    </div>
    <div class="step">
      <div class="step-num">6</div>
      <div class="step-line"></div>
      <div class="step-content"><h4>Identify resources needed</h4><p>Financial, human, and physical resources required to keep critical functions running.</p></div>
    </div>
    <div class="step">
      <div class="step-num">7</div>
      <div class="step-line"></div>
      <div class="step-content"><h4>Identify vital records & data backup</h4><p>Back up essential records (cloud, external drives, paper copies at alternate location). Cross-train staff for key roles.</p></div>
    </div>
    <div class="step">
      <div class="step-num">8</div>
      <div class="step-line"></div>
      <div class="step-content"><h4>Identify alternate business location</h4><p>Where will you operate if your primary site is damaged or inaccessible?</p></div>
    </div>
    <div class="step">
      <div class="step-num">9</div>
      <div class="step-line"></div>
      <div class="step-content"><h4>Write & implement the plan</h4><p>Use the Section 3 template. Brief all staff. Develop Mutual Aid Agreements with neighboring businesses.</p></div>
    </div>
    <div class="step">
      <div class="step-num">10</div>
      <div class="step-line"></div>
      <div class="step-content"><h4>Test, review & revise</h4><p>Run tabletop simulation exercises. Identify gaps. Revise the plan. Repeat after any real disaster event.</p></div>
    </div>
  </div>

  <div class="sec-title" style="font-size:1.1rem;"><span>📊</span> Business Impact Analysis — Key Questions</div>
  <div class="accordion">
    <div class="acc-header" onclick="toggleAcc(this)"><h4>What are my most critical business functions?</h4><span class="acc-arrow">▼</span></div>
    <div class="acc-body">Examples: Payroll, Accounts Receivable, Regulatory Reporting, Insurance Claims, Debt Obligations, Internal/External Communications, Recovery location set-up.</div>
  </div>
  <div class="accordion">
    <div class="acc-header" onclick="toggleAcc(this)"><h4>How much downtime can each function tolerate?</h4><span class="acc-arrow">▼</span></div>
    <div class="acc-body">Every critical function is time-sensitive. Rank them: High priority functions must be restored first. Low priority can wait. This guides resource allocation.</div>
  </div>
  <div class="accordion">
    <div class="acc-header" onclick="toggleAcc(this)"><h4>What legal/financial obligations must continue?</h4><span class="acc-arrow">▼</span></div>
    <div class="acc-body">Late or non-payment of statutory obligations (taxes, loan repayments) can lead to legal consequences or business failure. These must be identified upfront.</div>
  </div>
  <div class="accordion">
    <div class="acc-header" onclick="toggleAcc(this)"><h4>Is a vital record really vital?</h4><span class="acc-arrow">▼</span></div>
    <div class="acc-body"><ul><li>Is it required for business success?</li><li>Is it required for legal reasons?</li><li>Is it required by a regulatory agency?</li><li>Is it required to support recovery efforts?</li><li>Is it impossible to recreate?</li></ul></div>
  </div>
</section>

<!-- ══ FINANCIAL ══ -->
<section id="financial" class="section">
  <div class="sec-title"><span class="icon">💰</span> Financial Considerations</div>

  <div class="card-grid">
    <div class="card">
      <h3>💧 Liquidity</h3>
      <p>The more liquid the business (cash & short-term assets), the longer it can survive downtime. Less liquid businesses may need to borrow to fund BCP implementation.</p>
    </div>
    <div class="card">
      <h3>📈 Profitability Impact</h3>
      <p>How have disasters affected similar businesses' profits? Profit = Sales − Expenses − Tax. If disasters threaten profitability, implementing a BCP is a sound business investment.</p>
    </div>
    <div class="card">
      <h3>💳 Debt Servicing</h3>
      <p>How long will creditors wait if debt payments stop? Post-disaster, additional loans may be needed. Understand your debt obligations before disaster strikes.</p>
    </div>
    <div class="card">
      <h3>📥 Receivables</h3>
      <p>How long can the business survive on outstanding receivables? Determine the period before cash-flow becomes critical if customers cannot pay.</p>
    </div>
    <div class="card">
      <h3>👥 Customer Concentration</h3>
      <p>If 1–2 major customers are severely impacted, how does that affect you? High concentration = high risk. Consider including key customers in your BCP.</p>
    </div>
    <div class="card">
      <h3>🚚 Supplier Dependency</h3>
      <p>If a single major supplier is impacted, can you operate? Identify alternate suppliers. Key suppliers may need to be part of your BCP planning.</p>
    </div>
    <div class="card">
      <h3>🏆 Competitive Advantage</h3>
      <p>If you recover faster than competitors, you can capture their customers. Having a BCP can be a market differentiator — signal it to your customers.</p>
    </div>
    <div class="card">
      <h3>🛡 Insurance</h3>
      <p>Ensure policies are adequate and valid. Business Interruption Coverage offsets losses while operations are paused. Understand deductibles, limits, and exclusions.</p>
    </div>
  </div>

  <div class="sec-title" style="font-size:1.1rem; margin-top:1rem;"><span>🆕</span> Equipment / Capital Investment Questions</div>
  <div class="tag-row">
    <span class="tag-chip">How will new equipment be funded?</span>
    <span class="tag-chip">Loan vs. equity?</span>
    <span class="tag-chip">Does the benefit outweigh the cost?</span>
    <span class="tag-chip">Pass cost to consumer or absorb it?</span>
    <span class="tag-chip">What is the cash flow impact?</span>
    <span class="tag-chip">Phased implementation needed?</span>
  </div>
</section>

<!-- ══ FLASHCARDS ══ -->
<section id="flashcards" class="section">
  <div class="sec-title"><span class="icon">🃏</span> Flashcards</div>
  <p style="color:var(--muted); font-size:0.85rem; margin-bottom:1.5rem;">Click the card to reveal the answer. Use arrows to navigate.</p>

  <div class="flashcard-wrap" onclick="flipCard()">
    <div class="flashcard" id="flashcard">
      <div class="fc-face fc-front">
        <span class="fc-label">Term / Concept</span>
        <h3 id="fc-question">Loading...</h3>
        <span class="fc-hint">👆 Click to flip</span>
      </div>
      <div class="fc-face fc-back">
        <span class="fc-label">Answer / Definition</span>
        <p id="fc-answer"></p>
      </div>
    </div>
  </div>

  <div class="fc-nav" style="margin-top:1rem;">
    <button class="btn btn-ghost" onclick="prevCard()">← Prev</button>
    <span class="fc-counter" id="fc-counter">1 / 12</span>
    <button class="btn btn-ghost" onclick="nextCard()">Next →</button>
  </div>
</section>

<!-- ══ QUIZ ══ -->
<section id="quiz" class="section">
  <div class="sec-title"><span class="icon">🧠</span> Knowledge Quiz</div>
  <div class="quiz-container">
    <div class="quiz-progress" id="quiz-progress"></div>
    <div id="quiz-area"></div>
  </div>
</section>

<!-- ══ CHECKLIST ══ -->
<section id="checklist" class="section">
  <div class="sec-title"><span class="icon">✅</span> BCP Preparedness Checklist</div>
  <p style="color:var(--muted); font-size:0.85rem; margin-bottom:1rem;">Check off each item as you complete it for your business.</p>

  <div class="progress-bar-wrap">
    <div class="progress-bar-fill" id="cl-bar" style="width:0%"></div>
  </div>
  <p style="text-align:right; font-size:0.8rem; color:var(--muted); margin-top:-1rem; margin-bottom:1.2rem;" id="cl-count">0 / 20 complete</p>

  <div id="checklist-items"></div>
</section>

<script>
// ── NAV ──
function show(id) {
  document.querySelectorAll('.section').forEach(s => s.classList.remove('active'));
  document.querySelectorAll('nav button').forEach(b => b.classList.remove('active'));
  document.getElementById(id).classList.add('active');
  event.target.classList.add('active');
}

// ── ACCORDION ──
function toggleAcc(header) {
  const isOpen = header.classList.contains('open');
  document.querySelectorAll('.acc-header').forEach(h => h.classList.remove('open'));
  document.querySelectorAll('.acc-body').forEach(b => b.classList.remove('open'));
  if (!isOpen) {
    header.classList.add('open');
    header.nextElementSibling.classList.add('open');
  }
}

// ── FLASHCARDS ──
const cards = [
  { q: "What is a Business Continuity Plan (BCP)?", a: "A pre-planned set of procedures to ensure critical business functions continue or resume quickly after a disaster or disruption." },
  { q: "What is a Business Impact Analysis (BIA)?", a: "A detailed examination of potential disruptions and their impact on daily operations and long-term profitability. It identifies critical functions and their maximum tolerable downtime." },
  { q: "What is Site Vulnerability Analysis?", a: "An assessment of hazards your business faces based on its location — including storm surge, flooding, earthquakes, drought, climate change effects, and hazardous materials." },
  { q: "What is Business Interruption Coverage?", a: "An insurance product that offsets losses and covers overheads while a business is out of operation due to a covered hazard." },
  { q: "What is Cross-Training of Staff?", a: "Teaching employees how to perform another employee's job functions, ensuring critical operations can continue even if key staff are absent." },
  { q: "What is a Mutual Aid Agreement?", a: "A formal arrangement between businesses to assist one another with resources, space, or services during and after a disaster." },
  { q: "What is a Tabletop Simulation Exercise?", a: "An informal, classroom-style exercise where team members discuss their roles and responses to a hypothetical emergency scenario, guided by a facilitator." },
  { q: "Define: Liquidity (in BCP context)", a: "The amount of cash and short-term assets a business has. Higher liquidity allows longer survival during downtime and funds BCP implementation without borrowing." },
  { q: "Name 3 time-sensitive critical business functions", a: "Examples include: Payroll, Accounts Receivable, Regulatory Reporting, Insurance Claims, Debt Obligations, Internal/External Communications." },
  { q: "What are the 4 MSME constraint categories?", a: "Operational (equipment, personnel, ICT), Economic (finance, trade), Social (poverty, crime, education), and Technological (digital access, broadband)." },
  { q: "Which 3 Caribbean countries are classified as 'water scarce'?", a: "Barbados, Antigua & Barbuda, and St. Kitts & Nevis — each with less than 1,000 m³ of freshwater resources per capita per year." },
  { q: "When should the BCP plan be revised?", a: "After any real disaster event (record lessons learned), and after testing via simulation exercises where gaps or problems are identified." },
];

let fcIndex = 0;
function renderCard() {
  const card = cards[fcIndex];
  document.getElementById('fc-question').textContent = card.q;
  document.getElementById('fc-answer').textContent = card.a;
  document.getElementById('fc-counter').textContent = `${fcIndex + 1} / ${cards.length}`;
  document.getElementById('flashcard').classList.remove('flipped');
}
function flipCard() { document.getElementById('flashcard').classList.toggle('flipped'); }
function nextCard() { fcIndex = (fcIndex + 1) % cards.length; renderCard(); }
function prevCard() { fcIndex = (fcIndex - 1 + cards.length) % cards.length; renderCard(); }
renderCard();

// ── QUIZ ──
const questions = [
  { q: "What is the minimum number of employees for a 'Small Enterprise' under CDB definitions?", opts: ["3", "6", "10", "16"], ans: 1, exp: "A Small Enterprise has 6–15 employees. Micro = ≤5, Medium = 16–59." },
  { q: "In 2017, estimated economic damage to 4 CDB member countries from Hurricane Irma was approximately:", opts: ["USD $1 billion", "USD $3.3 billion", "USD $7 billion", "USD $500 million"], ans: 1, exp: "Hurricane Irma caused an estimated USD $3.307 billion in damage to four CDB member countries." },
  { q: "Which of these is NOT typically a time-sensitive critical business function in a BCP?", opts: ["Payroll", "Staff birthday celebrations", "Regulatory Reporting", "Accounts Receivable"], ans: 1, exp: "Staff birthday celebrations are not operationally critical. Payroll, regulatory reporting, and receivables are all time-sensitive." },
  { q: "A 'Tabletop Simulation Exercise' is:", opts: ["A physical drill evacuating all staff", "An informal discussion of emergency responses to a scenario", "A surprise unannounced disaster test", "A financial audit of disaster costs"], ans: 1, exp: "Tabletop exercises are informal, classroom-style discussions guided by a facilitator — cost-effective and relatively quick (a few hours)." },
  { q: "Business Interruption Coverage helps by:", opts: ["Rebuilding destroyed property", "Offsetting losses and covering overheads while operations are paused", "Replacing all staff who leave", "Paying government fines"], ans: 1, exp: "Business Interruption Coverage is specifically designed to cover operational costs while the business cannot operate due to a disaster." },
  { q: "Cross-training of staff is important for BCP because:", opts: ["It saves money on salaries", "It ensures alternate personnel can handle critical functions if staff are absent", "It satisfies regulatory requirements", "It replaces the need for a written plan"], ans: 1, exp: "Cross-training creates backup personnel for critical functions, ensuring operations can continue even when key employees are unavailable." },
  { q: "Which Caribbean country has a volcano known as 'the region's longest erupting volcano' (started 1995)?", opts: ["Jamaica", "St. Vincent", "Montserrat", "Grenada"], ans: 2, exp: "Soufrière Hills in Montserrat has been erupting since 1995, making it the region's longest erupting volcano." },
  { q: "A Mutual Aid Agreement is:", opts: ["A government subsidy program", "An arrangement between businesses to assist each other during a disaster", "A bank loan facility", "An insurance policy type"], ans: 1, exp: "Mutual Aid Agreements are formal arrangements between businesses to provide mutual support with resources, space, or services during and after disasters." },
  { q: "What does BIA stand for?", opts: ["Business Insurance Assessment", "Business Impact Analysis", "Business Interruption Act", "Basic Infrastructure Audit"], ans: 1, exp: "BIA = Business Impact Analysis — a detailed examination of potential disruptions and their effects on operations and profitability." },
  { q: "What should you do FIRST after the impact of a disaster, according to the BCP process?", opts: ["File insurance claims", "Assemble your BCP team and check employee welfare", "Call your suppliers", "Move to alternate location immediately"], ans: 1, exp: "The first step post-impact is to assemble your BCP team and check on employee welfare — people come before property." },
];

let qIndex = 0, answers = new Array(questions.length).fill(null), score = 0;

function renderQuiz() {
  const prog = document.getElementById('quiz-progress');
  prog.innerHTML = questions.map((_, i) => {
    let cls = 'quiz-dot';
    if (answers[i] !== null) cls += answers[i] ? ' correct' : ' wrong';
    return `<div class="${cls}"></div>`;
  }).join('');

  if (qIndex >= questions.length) {
    const pct = Math.round((score / questions.length) * 100);
    document.getElementById('quiz-area').innerHTML = `
      <div class="score-card">
        <div class="score-num">${pct}%</div>
        <div class="score-label">${score} of ${questions.length} correct</div>
        <p style="margin-top:1rem; color:var(--muted); font-size:0.85rem;">
          ${pct >= 80 ? '🎉 Excellent! You have a strong grasp of BCP fundamentals.' : pct >= 60 ? '👍 Good effort! Review the sections on areas you missed.' : '📖 Keep studying! Review the Hazards and Planning sections.'}
        </p>
        <button class="btn" style="margin-top:1.5rem;" onclick="restartQuiz()">Restart Quiz</button>
      </div>`;
    return;
  }

  const q = questions[qIndex];
  document.getElementById('quiz-area').innerHTML = `
    <div class="question-card">
      <div class="q-num">Question ${qIndex + 1} of ${questions.length}</div>
      <h3>${q.q}</h3>
      <div class="options">
        ${q.opts.map((o, i) => `<button class="option" onclick="selectAnswer(${i})">${o}</button>`).join('')}
      </div>
      <div class="feedback" id="feedback"></div>
    </div>
    <div class="quiz-nav">
      <span style="color:var(--muted);font-size:0.8rem;">Score: ${score}/${qIndex}</span>
      <button class="btn" id="next-btn" style="display:none;" onclick="nextQuestion()">Next →</button>
    </div>`;
}

function selectAnswer(i) {
  const q = questions[qIndex];
  const opts = document.querySelectorAll('.option');
  opts.forEach(o => o.disabled = true);
  const isCorrect = i === q.ans;
  opts[i].classList.add(isCorrect ? 'correct' : 'wrong');
  opts[q.ans].classList.add('correct');
  if (isCorrect) score++;
  answers[qIndex] = isCorrect;
  const fb = document.getElementById('feedback');
  fb.classList.add('show', isCorrect ? 'correct' : 'wrong');
  fb.innerHTML = (isCorrect ? '✅ Correct! ' : '❌ Incorrect. ') + q.exp;
  document.getElementById('next-btn').style.display = 'block';
  renderDots();
}

function renderDots() {
  document.getElementById('quiz-progress').innerHTML = questions.map((_, i) => {
    let cls = 'quiz-dot';
    if (answers[i] !== null) cls += answers[i] ? ' correct' : ' wrong';
    return `<div class="${cls}"></div>`;
  }).join('');
}

function nextQuestion() { qIndex++; renderQuiz(); }
function restartQuiz() { qIndex = 0; score = 0; answers.fill(null); renderQuiz(); }
renderQuiz();

// ── CHECKLIST ──
const clItems = [
  "My business insurance policy is valid and coverage is adequate",
  "I have Business Interruption Coverage",
  "I have a Mutual Aid Agreement with at least one other business",
  "My business data is backed up regularly",
  "Data backups are stored at an alternate location or in the cloud",
  "I have completed a Site Vulnerability Analysis",
  "I have identified all hazards that could affect my business",
  "I have completed a Business Impact Analysis (BIA)",
  "I have identified my top 5 most critical business functions",
  "I have determined maximum tolerable downtime for each critical function",
  "I have a contact list for all staff (Table 8)",
  "I have a contact list for all key suppliers (Table 9)",
  "Staff are cross-trained to cover critical functions",
  "I have identified an alternate business location",
  "Vital records are identified and backed up",
  "I have a clear communication plan for staff and customers",
  "My BCP has been written using the Section 3 template",
  "All employees have been briefed on the plan",
  "I have tested the plan using a tabletop simulation exercise",
  "The plan has been revised based on testing results",
];
let clState = new Array(clItems.length).fill(false);

function renderChecklist() {
  const container = document.getElementById('checklist-items');
  container.innerHTML = clItems.map((item, i) => `
    <div class="checklist-item ${clState[i] ? 'checked' : ''}" onclick="toggleCheck(${i})">
      <div class="check-box">${clState[i] ? '✓' : ''}</div>
      <span class="check-text ${clState[i] ? 'checked' : ''}">${item}</span>
    </div>`).join('');
  const done = clState.filter(Boolean).length;
  document.getElementById('cl-bar').style.width = (done / clItems.length * 100) + '%';
  document.getElementById('cl-count').textContent = `${done} / ${clItems.length} complete`;
}

function toggleCheck(i) {
  clState[i] = !clState[i];
  renderChecklist();
}
renderChecklist();
</script>
</body>
</html>
