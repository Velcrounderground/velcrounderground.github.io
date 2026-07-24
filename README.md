<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Velcro Underground</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Space+Mono:ital,wght@0,400;0,700;1,400&display=swap" rel="stylesheet">
<style>
  :root{
    --bg: #07070a;
    --bg-2: #0d0713;
    --magenta: #ff1f8f;
    --cyan: #17f2ff;
    --acid: #ccff2e;
    --text: #f2ede3;
    --muted: #948f9c;
    --line: rgba(242,237,227,0.12);
  }

  *{ box-sizing: border-box; }
  html{ scroll-behavior: smooth; }

  body{
    margin:0;
    background: var(--bg);
    color: var(--text);
    font-family: 'Space Mono', monospace;
    overflow-x: hidden;
  }

  .display{
    font-family: 'Bebas Neue', sans-serif;
    letter-spacing: 0.04em;
    line-height: 0.9;
  }

  a{ color: inherit; }

  /* grain overlay */
  .grain{
    position: fixed; inset: 0; z-index: 40; pointer-events: none;
    opacity: 0.05; mix-blend-mode: overlay;
    background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='120' height='120'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='2' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
  }

  /* NAV */
  nav{
    position: fixed; top:0; left:0; right:0; z-index: 30;
    display:flex; justify-content: space-between; align-items:center;
    padding: 22px 5vw;
    font-size: 12px; letter-spacing: 0.18em; text-transform: uppercase;
    mix-blend-mode: difference;
  }
  nav .mark{ font-family:'Bebas Neue',sans-serif; font-size: 20px; letter-spacing:0.08em; }
  nav ul{ display:flex; gap: 28px; list-style:none; margin:0; padding:0; }
  nav a{ text-decoration:none; color: var(--text); opacity:0.8; transition: opacity 0.2s, color 0.2s; }
  nav a:hover{ opacity:1; color: var(--cyan); }

  /* HERO */
  .hero{
    position: relative;
    height: 100svh;
    display:flex; flex-direction: column; align-items:center; justify-content:center;
    text-align:center;
    background: radial-gradient(ellipse at 50% 30%, var(--bg-2), var(--bg) 70%);
    overflow: hidden;
  }

  .beams{ position:absolute; inset:-20%; z-index:1; opacity:0.55; }
  .beam{
    position:absolute; top:50%; left:50%;
    width: 2px; height: 140vmax;
    transform-origin: top center;
    filter: blur(1px);
  }
  .beam.b1{ background: linear-gradient(to bottom, var(--magenta), transparent 55%); animation: sweep 14s linear infinite; }
  .beam.b2{ background: linear-gradient(to bottom, var(--cyan), transparent 60%); animation: sweep 19s linear infinite reverse; }
  .beam.b3{ background: linear-gradient(to bottom, var(--acid), transparent 50%); animation: sweep 23s linear infinite; animation-delay: -6s; }
  .beam.b4{ background: linear-gradient(to bottom, var(--magenta), transparent 45%); animation: sweep 17s linear infinite reverse; animation-delay: -10s; }

  @keyframes sweep{
    from{ transform: translate(-50%,0) rotate(0deg); }
    to{ transform: translate(-50%,0) rotate(360deg); }
  }

  .hero-inner{ position:relative; z-index: 5; padding: 0 20px; }

  .kicker{
    font-size: 11px; letter-spacing: 0.35em; text-transform: uppercase;
    color: var(--acid); margin-bottom: 18px; opacity:0.9;
  }

  h1.logo{
    font-size: clamp(52px, 13vw, 168px);
    margin: 0;
    color: var(--text);
    text-shadow:
      0 0 6px rgba(242,237,227,0.6),
      0 0 22px var(--magenta),
      0 0 55px var(--magenta);
  }
  h1.logo span{
    display:block;
    color: var(--cyan);
    text-shadow: 0 0 6px rgba(23,242,255,0.7), 0 0 22px var(--cyan), 0 0 55px var(--cyan);
  }
  h1.logo.flicker-off{ text-shadow: none; opacity: 0.35; }

  .tagline{
    margin: 26px auto 0; max-width: 520px;
    color: var(--muted); font-size: 14px; line-height: 1.7;
  }

  .cta-row{ margin-top: 40px; display:flex; gap:16px; justify-content:center; flex-wrap:wrap; }
  .btn{
    display:inline-block; padding: 14px 30px;
    border: 1px solid var(--line); border-radius: 2px;
    text-decoration:none; font-size:12px; letter-spacing:0.18em; text-transform:uppercase;
    transition: all 0.25s ease;
  }
  .btn.solid{ background: var(--magenta); border-color: var(--magenta); color:#0a0a0a; font-weight:700; }
  .btn.solid:hover{ background: var(--cyan); border-color: var(--cyan); box-shadow: 0 0 30px var(--cyan); }
  .btn.ghost:hover{ border-color: var(--cyan); color: var(--cyan); box-shadow: 0 0 20px rgba(23,242,255,0.35); }

  .scroll-cue{
    position:absolute; bottom: 34px; left:50%; transform: translateX(-50%);
    font-size: 10px; letter-spacing:0.3em; color: var(--muted); text-transform:uppercase;
    display:flex; flex-direction:column; align-items:center; gap:8px; z-index:5;
  }
  .scroll-cue .line{ width:1px; height:34px; background: linear-gradient(var(--muted), transparent); animation: pulse 2s ease-in-out infinite; }
  @keyframes pulse{ 0%,100%{ opacity:0.3; } 50%{ opacity:1; } }

  /* SECTIONS */
  section{ padding: 120px 8vw; position:relative; }
  .eyebrow{
    font-size: 11px; letter-spacing: 0.3em; text-transform: uppercase; color: var(--acid);
    margin: 0 0 20px;
  }
  h2{
    font-family:'Bebas Neue',sans-serif; font-size: clamp(36px, 6vw, 76px);
    margin: 0 0 34px; letter-spacing:0.02em;
  }

  /* ABOUT */
  .about{ border-top: 1px solid var(--line); }
  .about-grid{ display:grid; grid-template-columns: 1fr 1fr; gap: 60px; align-items:start; }
  .about p{ color: var(--muted); font-size:15px; line-height:1.9; margin: 0 0 18px; }
  .about strong{ color: var(--text); }
  .stat-list{ display:flex; flex-direction:column; gap: 22px; }
  .stat{ display:flex; justify-content:space-between; border-bottom: 1px solid var(--line); padding-bottom: 14px; }
  .stat .k{ color: var(--muted); font-size:12px; letter-spacing:0.1em; text-transform:uppercase; }
  .stat .v{ font-family:'Bebas Neue',sans-serif; font-size: 22px; color: var(--cyan); }

  /* SETS */
  .sets{ background: linear-gradient(180deg, transparent, rgba(255,31,143,0.04), transparent); border-top: 1px solid var(--line); }
  .set-grid{ display:grid; grid-template-columns: repeat(3, 1fr); gap: 1px; background: var(--line); border: 1px solid var(--line); }
  .set-card{
    background: var(--bg); padding: 34px 28px; min-height: 240px;
    display:flex; flex-direction:column; justify-content:space-between;
    transition: background 0.25s ease;
  }
  .set-card:hover{ background: #0c0810; }
  .set-card .tag{ font-size:11px; color: var(--magenta); letter-spacing:0.15em; text-transform:uppercase; }
  .set-card h3{ font-family:'Bebas Neue',sans-serif; font-size: 30px; margin: 16px 0 10px; }
  .set-card p{ color: var(--muted); font-size:13px; line-height:1.6; margin:0; }
  .set-card .play{ margin-top: 20px; font-size:12px; letter-spacing:0.15em; color: var(--cyan); text-decoration:none; }

  /* PLAYDATES */
  .playdates{ border-top: 1px solid var(--line); }
  .date-row{
    display:grid; grid-template-columns: 90px 1fr auto auto; gap: 24px; align-items:center;
    padding: 22px 0; border-bottom: 1px solid var(--line);
  }
  .date-row .d{ font-family:'Bebas Neue',sans-serif; font-size: 28px; color: var(--acid); }
  .date-row .d small{ display:block; font-family:'Space Mono',monospace; font-size:10px; color:var(--muted); letter-spacing:0.1em; }
  .date-row .venue{ font-size: 14px; }
  .date-row .venue .city{ color: var(--muted); font-size:12px; display:block; margin-top:4px; letter-spacing:0.05em;}
  .date-row .status{ font-size: 11px; letter-spacing:0.15em; text-transform:uppercase; color: var(--muted); }
  .date-row .status.open{ color: var(--cyan); }
  .date-row a.tix{ font-size:11px; letter-spacing:0.12em; text-transform:uppercase; border:1px solid var(--line); padding:8px 16px; text-decoration:none; }
  .date-row a.tix:hover{ border-color: var(--magenta); color: var(--magenta); }
  .more-note{ margin-top: 26px; color: var(--muted); font-size: 13px; }

  /* CONTACT / FOOTER */
  footer{
    border-top: 1px solid var(--line);
    padding: 100px 8vw 50px;
    background: linear-gradient(180deg, transparent, var(--bg-2));
  }
  .contact-grid{ display:grid; grid-template-columns: 1.2fr 1fr; gap: 60px; }
  .contact-grid h2{ margin-bottom: 20px; }
  .contact-list{ list-style:none; padding:0; margin: 0 0 30px; }
  .contact-list li{ margin-bottom: 14px; font-size:14px; }
  .contact-list .k{ color: var(--muted); display:block; font-size:11px; letter-spacing:0.15em; text-transform:uppercase; margin-bottom:4px; }
  .contact-list a{ text-decoration:none; color: var(--text); border-bottom:1px solid var(--line); }
  .contact-list a:hover{ color: var(--magenta); border-color: var(--magenta); }
  .socials{ display:flex; gap: 20px; }
  .socials a{ font-size:12px; letter-spacing:0.15em; text-transform:uppercase; text-decoration:none; color:var(--muted); }
  .socials a:hover{ color: var(--cyan); }
  .fine{ margin-top: 70px; display:flex; justify-content:space-between; color: var(--muted); font-size:11px; letter-spacing:0.05em; flex-wrap:wrap; gap:10px; }

  @media (max-width: 860px){
    .about-grid, .contact-grid{ grid-template-columns: 1fr; }
    .set-grid{ grid-template-columns: 1fr; }
    .date-row{ grid-template-columns: 60px 1fr; }
    .date-row .status, .date-row a.tix{ grid-column: 2; justify-self:start; }
    nav ul{ gap: 16px; }
  }

  @media (prefers-reduced-motion: reduce){
    .beam, .scroll-cue .line{ animation: none !important; }
  }
</style>
</head>
<body>

<div class="grain"></div>

<nav>
  <div class="mark">VELCRO ⌁ UNDERGROUND</div>
  <ul>
    <li><a href="#about">About</a></li>
    <li><a href="#sets">Sets</a></li>
    <li><a href="#playdates">Playdates</a></li>
    <li><a href="#contact">Booking</a></li>
  </ul>
</nav>

<section class="hero">
  <div class="beams">
    <div class="beam b1"></div>
    <div class="beam b2"></div>
    <div class="beam b3"></div>
    <div class="beam b4"></div>
  </div>
  <div class="hero-inner">
    <div class="kicker">Tech House / After Hours</div>
    <h1 class="logo" id="mainLogo">VELCRO<span>UNDERGROUND</span></h1>
    <p class="tagline">Low ceilings, and low standards. Hear the sounds of the subtle velcro humming into your ears, shaking your body.</p>
    <div class="cta-row">
      <a href="#playdates" class="btn solid">See Playdates</a>
      <a href="#contact" class="btn ghost">Book Us</a>
    </div>
  </div>
  <div class="scroll-cue"><div class="line"></div>SCROLL</div>
</section>

<section class="about" id="about">
  <div class="eyebrow">01 — The Project</div>
  <div class="about-grid">
    <div>
      <h2>Sound from<br>below street level.</h2>
      <p><strong>Velcro Underground</strong> is a tech house project built on rooms nobody advertises — the ones you find out about the night before. Rolling low-end, hypnotic groove, and just enough grit to remind you it's real.</p>
      <p>Every set is built to hold a room from first record to sunrise, whether that room holds forty people or four thousand.</p>
    </div>
    <div class="stat-list">
      <div class="stat"><span class="k">Based</span><span class="v">Underground, Everywhere</span></div>
      <div class="stat"><span class="k">Sound</span><span class="v">Psyc House / Groove</span></div>
      <div class="stat"><span class="k">Sets Played</span><span class="v">30</span></div>
      <div class="stat"><span class="k">Avg Set Length</span><span class="v">3 Hours</span></div>
    </div>
  </div>
</section>

<section class="sets" id="sets">
  <div class="eyebrow">02 — Latest Sets</div>
  <h2>Selects & Sessions</h2>
  <div class="set-grid">
    <div class="set-card">
      <div>
        <span class="tag">Live Recording</span>
        <h3>Basement Session Vol. 1</h3>
        <p>Raw room recording, deep and rolling from open to close.</p>
      </div>
      <a class="play" href="#">▶ Listen — Add your link</a>
    </div>
    <div class="set-card">
      <div>
        <span class="tag">Mix</span>
        <h3>4AM Selects</h3>
        <p>The stretch of night where the groove takes over completely.</p>
      </div>
      <a class="play" href="#">▶ Listen — Add your link</a>
    </div>
    <div class="set-card">
      <div>
        <span class="tag">Live Recording</span>
        <h3>Warehouse Tape 003</h3>
        <p>Recorded live, unedited — exactly how the room heard it.</p>
      </div>
      <a class="play" href="#">▶ Listen — Add your link</a>
    </div>
  </div>
</section>

<section class="playdates" id="playdates">
  <div class="eyebrow">03 — Upcoming</div>
  <h2>Playdates</h2>

  <div class="date-row">
    <div class="d">TBA<small>2026</small></div>
    <div class="venue">Venue Name<span class="city">City, Country</span></div>
    <div class="status open">Tickets Open</div>
    <a class="tix" href="#">Tickets</a>
  </div>

<footer id="contact">
  <div class="eyebrow">04 — Get In Touch</div>
  <div class="contact-grid">
    <div>
      <h2>Booking &<br>Business</h2>
      <ul class="contact-list">
        <li><span class="k">Booking / Playdates</span><a href="mailto:velcrounderground1@gmail.com">velcrounderground1@gmail.com</a></li>
        <li><span class="k">General / Press</span><a href="mailto:velcrounderground1@gmail.com">velcrounderground1@gmail.com</a></li>
      </ul>
      <div class="socials">
        <a href="#">Instagram</a>
        <a href="#">SoundCloud</a>
        <a href="#">Resident Advisor</a>
      </div>
    </div>
    <div>
      <p style="color:var(--muted); font-size:13px; line-height:1.8;">
        For booking inquiries, please include the venue, date, city, and payment please. We reply to every real offer — usually at sunrise.
      </p>
    </div>
  </div>
  <div class="fine">
    <span>© 2026 Velcro Underground. All rights reserved.</span>
    <span>Site built for velcrounderground.com</span>
  </div>
</footer>

<script>
  // irregular neon flicker on the main logo, like an aging sign
  const logo = document.getElementById('mainLogo');
  function scheduleFlicker(){
    const delay = 2200 + Math.random() * 5000;
    setTimeout(() => {
      logo.classList.add('flicker-off');
      setTimeout(() => {
        logo.classList.remove('flicker-off');
        scheduleFlicker();
      }, 70 + Math.random() * 90);
    }, delay);
  }
  if (!window.matchMedia('(prefers-reduced-motion: reduce)').matches) {
    scheduleFlicker();
  }
</script>

</body>
</html>

