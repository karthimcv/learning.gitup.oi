<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Jarvis — Personal Portfolio</title>
  <meta name="description" content="A clean, animated personal portfolio template in a single HTML file." />
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;800&display=swap" rel="stylesheet">
  <style>
    :root{
      --bg: #0b1020;
      --panel: rgba(5, 5, 5, 0.05);
      --text: #e6e9f2;
      --muted: #a6accd;
      --brand: #7c5cff;
      --brand-2: #00e5ff;
      --accent: #15ffab;
      --ring: rgba(124,92,255,.35);
      --radius: 18px;
      --shadow: 0 10px 30px rgba(0,0,0,.25);
    }

    *{ box-sizing:border-box; }
    html,body{ margin:0; height:100%; }
    body{
      font-family: Inter, system-ui, -apple-system, Segoe UI, Roboto, Arial, "Noto Sans", "Apple Color Emoji", "Segoe UI Emoji";
      background: radial-gradient(1200px 700px at 80% -20%, rgba(124,92,255,.35), transparent 60%),
                  radial-gradient(900px 600px at -10% 10%, rgba(0,229,255,.25), transparent 60%),
                  var(--bg);
      color: var(--text);
      line-height: 1.6;
      scroll-behavior: smooth;
      overflow-x: hidden;
    }

    /* ===== Navigation ===== */
    .nav{
      position: sticky; top:0; z-index: 50;
      background: linear-gradient(to bottom, rgba(11,16,32,.9), rgba(11,16,32,.55));
      backdrop-filter: blur(12px);
      border-bottom: 1px solid rgba(255,255,255,.06);
    }
    .nav-inner{ max-width:1100px; margin:0 auto; display:flex; align-items:center; justify-content:space-between; padding:14px 18px; }
    .brand{ font-weight:800; letter-spacing:.5px; }
    .brand .dot{ color: var(--brand); }
    .nav a{ color: var(--muted); text-decoration:none; margin-left:18px; font-weight:600; font-size:14px; }
    .nav a:hover{ color:var(--text); }

    /* ===== Hero ===== */
    .hero{
      position: relative; isolation:isolate; min-height: 88svh; display:grid; place-items:center; padding: 80px 18px 60px;
    }
    .hero-grid{ max-width:1100px; width:100%; display:grid; grid-template-columns: 1.2fr 1fr; gap:40px; align-items:center; }
    .headline{ font-size: clamp(28px, 4.2vw, 56px); line-height:1.1; font-weight:800; letter-spacing:-.02em; }
    .headline span{ background: linear-gradient(90deg, var(--brand), var(--brand-2)); -webkit-background-clip:text; background-clip:text; color:transparent; }
    .subhead{ color:var(--muted); margin-top:14px; font-size: clamp(14px, 1.7vw, 18px); }
    .cta-row{ margin-top:28px; display:flex; gap:14px; flex-wrap:wrap; }
    .btn{
      appearance:none; border:0; cursor:pointer; font-weight:700; padding:12px 18px; border-radius: var(--radius);
      transition: transform .15s ease, box-shadow .15s ease, background .15s ease, color .15s ease;
    }
    .btn-primary{ background: linear-gradient(90deg, var(--brand), var(--brand-2)); color:#0b1020; box-shadow: 0 8px 24px var(--ring); }
    .btn-primary:hover{ transform: translateY(-2px); }
    .btn-ghost{ background: var(--panel); color: var(--text); border:1px solid rgba(255,255,255,.08); }
    .btn-ghost:hover{ background: rgba(255,255,255,.08); }

    /* Decorative blob */
    .blob{
      position:absolute; right:-120px; top: -120px; width: 420px; height: 420px; filter: blur(30px); opacity:.55; z-index:-1;
      background: conic-gradient(from 180deg at 50% 50%, var(--brand), var(--brand-2), var(--accent), var(--brand));
      border-radius: 36% 64% 57% 43% / 43% 48% 52% 57%;
      animation: blob 18s ease-in-out infinite;
    }
    @keyframes blob{
      0%,100%{ transform: translate(0,0) rotate(0deg) scale(1); }
      33%{ transform: translate(-10px, 20px) rotate(8deg) scale(1.05); }
      66%{ transform: translate(8px, -16px) rotate(-6deg) scale(0.98); }
    }

    /* Hero card preview */
    .preview{
      background: linear-gradient(180deg, rgba(255,255,255,.06), rgba(255,255,255,.03));
      border: 1px solid rgba(255,255,255,.08);
      border-radius: calc(var(--radius) + 10px);
      box-shadow: var(--shadow);
      padding: 18px; display:grid; gap:14px;
      transform: perspective(900px) rotateY(0deg) rotateX(0deg);
      transition: transform .25s ease;
    }
    .preview:hover{ transform: perspective(900px) rotateY(3deg) rotateX(-2deg); }
    .preview .row{ display:flex; gap:12px; }
    .chip{ font-size:12px; padding:6px 10px; border-radius:999px; background: rgba(21,255,171,.15); border:1px solid rgba(21,255,171,.35); color:#caffea; }
    .codeblock{
      font-family: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, "Liberation Mono", monospace; font-size: 13px;
      background: #0b0f1a; border:1px solid rgba(255,255,255,.06); border-radius: 14px; padding:14px; color:#cde1ff;
    }

    /* ===== Sections ===== */
    section{ padding: 80px 18px; }
    .wrap{ max-width:1100px; margin:0 auto; }
    .section-title{ font-size: clamp(22px, 3vw, 34px); font-weight:800; margin-bottom:10px; }
    .section-note{ color:var(--muted); margin-bottom: 26px; }

    .grid-3{ display:grid; grid-template-columns: repeat(3, 1fr); gap:18px; }
    .card{
      background: var(--panel); border:1px solid rgba(255,255,255,.08); border-radius: var(--radius); padding:18px; box-shadow: var(--shadow);
      transition: transform .18s ease, background .18s ease, border-color .18s ease;
    }
    .card:hover{ transform: translateY(-6px); border-color: rgba(124,92,255,.45); background: rgba(255,255,255,.07); }

    .projects .item img{ width:100%; height:180px; object-fit:cover; border-radius: 12px; border:1px solid rgba(255,255,255,.06); }
    .projects .item h3{ margin:10px 0 6px; font-size:18px; }
    .projects .item p{ color:var(--muted); margin:0 0 10px; }

    /* Skills */
    .skills .row{ display:grid; grid-template-columns: 1fr 1fr; gap:18px; }
    .bar{ background:#0e1426; border-radius:12px; height:10px; overflow:hidden; border:1px solid rgba(255,255,255,.06); }
    .fill{ height:100%; width:0; background: linear-gradient(90deg, var(--brand), var(--accent)); border-radius:inherit; box-shadow: inset 0 0 10px rgba(124,92,255,.4); }

    /* Contact */
    .contact form{ display:grid; gap:12px; }
    .input{
      background:#0e1426; color:var(--text); border:1px solid rgba(255,255,255,.08); border-radius:12px; padding:12px 14px; font: inherit;
    }
    textarea.input{ min-height:120px; resize: vertical; }

    /* Footer */
    footer{ padding: 26px 18px 60px; color: var(--muted); text-align:center; }

    /* ===== Reveal Animations ===== */
    .reveal{ opacity:0; transform: translateY(14px); filter: saturate(.7); }
    .reveal.show{ opacity:1; transform:none; filter: none; transition: opacity .7s ease, transform .7s ease, filter .7s ease; }

    /* Back to top */
    .to-top{ position: fixed; right: 18px; bottom: 18px; padding:10px 12px; border-radius:999px; background: var(--panel); border:1px solid rgba(255,255,255,.12); display:none; }
    .to-top.show{ display:inline-flex; }

    /* ===== Responsive ===== */
    @media (max-width: 900px){
      .hero-grid{ grid-template-columns: 1fr; }
      .grid-3{ grid-template-columns: 1fr; }
      .skills .row{ grid-template-columns: 1fr; }
      .nav a{ margin-left:12px; }
    }

    /* ===== Accessibility: reduce motion ===== */
    @media (prefers-reduced-motion: reduce){
      *{ animation: none !important; transition: none !important; }
      .blob{ display:none; }
    }
  </style>
</head>
<body>
  <!-- ===== NAV ===== -->
  <nav class="nav" aria-label="Primary">
    <div class="nav-inner">
      <div class="brand" aria-label="Site name">karthikeyan<span class="dot">.</span>dev</div>
      <div class="links" role="navigation">
        <a href="#about">About</a>
        <a href="#projects">Projects</a>
        <a href="#skills">Skills</a>
        <a href="#contact">Contact</a>
      </div>
    </div>
  </nav>

  <!-- ===== HERO ===== -->
  <header class="hero" id="home">
    <div class="blob" aria-hidden="true"></div>
    <div class="hero-grid wrap">
      <div class="copy">
        <h1 class="headline reveal">Hello, I'm <span>Karthikeyan</span> — Bcome A Front‑End Developer</h1>
        <p class="subhead reveal" style="transition-delay:.1s">I learning-craft a clean, fast, accessible websites with delightful micro‑interactions. Available for freelance projects & internships.</p>
        <div class="cta-row reveal" style="transition-delay:.2s">
          <a class="btn btn-primary" href="#projects">See Projects</a>
          <a class="btn btn-ghost" href="#contact">Hire Me</a>
        </div>
        <div class="row reveal" style="margin-top:14px; gap:8px; align-items:center; transition-delay:.3s">
          <span class="chip">HTML</span>
          <span class="chip" style="background:rgba(124,92,255,.15); border-color:rgba(124,92,255,.4); color:#e6dcff;">CSS</span>
          <span class="chip" style="background:rgba(0,229,255,.15); border-color:rgba(0,229,255,.4); color:#e6fbff;">JavaScript</span>
        </div>
      </div>
      <div class="preview reveal" style="transition-delay:.15s">
        <div class="row" style="justify-content:space-between; align-items:center;">
          <div style="display:flex; gap:8px; align-items:center;">
            <div style="width:10px; height:10px; background:#ff6b6b; border-radius:999px"></div>
            <div style="width:10px; height:10px; background:#ffd93d; border-radius:999px"></div>
            <div style="width:10px; height:10px; background:#6bff95; border-radius:999px"></div>
          </div>
          <small style="color:var(--muted)">preview.html</small>
        </div>
        <div class="codeblock" aria-label="Sample code">
<pre><code>&lt;button class="btn"&gt;Hover me&lt;/button&gt;

.btn{
  background: linear-gradient(90deg, #7c5cff, #00e5ff);
  transform: translateY(0);
}
.btn:hover{ transform: translateY(-2px); }
</code></pre>
        </div>
      </div>
    </div>
  </header>

  <!-- ===== ABOUT ===== -->
  <section id="about" class="about">
    <div class="wrap">
      <h2 class="section-title reveal">About Me</h2>
      <p class="section-note reveal" style="transition-delay:.1s">Passionate developer focused on building beautiful, accessible interfaces. I enjoy solving problems, polishing details, and learning new technologies.</p>

      <div class="grid-3">
        <article class="card reveal" style="transition-delay:.05s">
          <h3>What I Do</h3>
          <p>I design and build responsive websites & landing pages, turn Figma designs into code, and optimize performance.</p>
        </article>
        <article class="card reveal" style="transition-delay:.1s">
          <h3>Toolbox</h3>
          <p> learning HTML, CSS, JavaScript, Git/GitHub(new comer), React (basics), and a sprinkle of GSAP/Scroll animations.</p>
        </article>
        <article class="card reveal" style="transition-delay:.15s">
          <h3>Currently Learning</h3>
          <p> pro in hdml,java(basic) , phython(basic).etc..</p>
        </article>
      </div>
    </div>
  </section>

  <!-- ===== PROJECTS ===== -->
  <section id="projects" class="projects">
    <div class="wrap">
      <h2 class="section-title reveal">Selected Projects</h2>
      <p class="section-note reveal" style="transition-delay:.1s">A few things I’ve built recently. Replace these with your own screenshots and links.</p>

      <div class="grid-3">
        <article class="item card reveal" style="transition-delay:.05s">
          <img src="https://images.unsplash.com/photo-1526378722484-bd91ca387e72?q=80&w=1200&auto=format&fit=crop" alt="Dashboard project preview" loading="lazy">
          <h3>Analytics Dashboard</h3>
          <p>Responsive dashboard UI with charts, dark mode, and smooth transitions.</p>
          <div class="cta-row">
            <a class="btn btn-ghost" href="#" aria-label="Live demo">Live</a>
            <a class="btn btn-ghost" href="#" aria-label="Source code">Code</a>
          </div>
        </article>

        <article class="item card reveal" style="transition-delay:.1s">
          <img src="https://images.unsplash.com/photo-1542744173-05336fcc7ad4?q=80&w=1200&auto=format&fit=crop" alt="Landing page project preview" loading="lazy">
          <h3>Product Landing</h3>
          <p>Clean marketing page with scroll‑reveals and performance‑focused images.</p>
          <div class="cta-row">
            <a class="btn btn-ghost" href="#">Live</a>
            <a class="btn btn-ghost" href="#">Code</a>
          </div>
        </article>

        <article class="item card reveal" style="transition-delay:.15s">
          <img src="https://images.unsplash.com/photo-1498050108023-c5249f4df085?q=80&w=1200&auto=format&fit=crop" alt="Portfolio project preview" loading="lazy">
          <h3>Dev Portfolio</h3>
          <p>Personal site template with modular components, theming, and micro‑interactions.</p>
          <div class="cta-row">
            <a class="btn btn-ghost" href="#">Live</a>
            <a class="btn btn-ghost" href="#">Code</a>
          </div>
        </article>
      </div>
    </div>
  </section>

  <!-- ===== SKILLS ===== -->
  <section id="skills" class="skills">
    <div class="wrap">
      <h2 class="section-title reveal">Skills</h2>
      <p class="section-note reveal" style="transition-delay:.1s">Bars animate in when visible. Edit percentages in the HTML <code>data-level</code> attributes.</p>

      <div class="row">
        <div class="card reveal" style="transition-delay:.05s">
          <strong>HTML</strong>
          <div class="bar" aria-label="HTML skill level"><div class="fill" data-level="50"></div></div>
        </div>
        <div class="card reveal" style="transition-delay:.1s">
          <strong>CSS</strong>
          <div class="bar" aria-label="CSS skill level"><div class="fill" data-level="10"></div></div>
        </div>
        <div class="card reveal" style="transition-delay:.15s">
          <strong>JavaScript</strong>
          <div class="bar" aria-label="JavaScript skill level"><div class="fill" data-level="10"></div></div>
        </div>
        <div class="card reveal" style="transition-delay:.2s">
          <strong>React</strong>
          <div class="bar" aria-label="React skill level"><div class="fill" data-level="40"></div></div>
        </div>
      </div>
    </div>
  </section>

  <!-- ===== CONTACT ===== -->
  <section id="contact" class="contact">
    <div class="wrap">
      <h2 class="section-title reveal">Contact</h2>
      <p class="section-note reveal" style="transition-delay:.1s">Let's collaborate! This form uses mailto for quick demos — swap it with a real backend later.</p>

      <form class="card reveal" style="transition-delay:.15s" action="mailto:yourmail@example.com" method="post" enctype="text/plain">
        <input class="input" type="text" name="name" placeholder="Your name" required>
        <input class="input" type="email" name="email" placeholder="Email address" required>
        <textarea class="input" name="message" placeholder="Tell me about your project" required></textarea>
        <button class="btn btn-primary" type="submit">Send Message</button>
      </form>
    </div>
  </section>

  <!-- ===== FOOTER ===== -->
  <footer>
    <small>© <span id="year"></span> Karthikeyan • Built with HTML/CSS/JS • <a href="#home" style="color:inherit; text-decoration:underline">Back to top</a></small>
  </footer>

  <button class="to-top" id="toTop" aria-label="Back to top">↑</button>

  <!-- ===== SCRIPTS ===== -->
  <script>
    // Intersection Observer for reveal-on-scroll
    const observer = new IntersectionObserver((entries)=>{
      entries.forEach((entry)=>{
        if(entry.isIntersecting){ entry.target.classList.add('show'); }
      })
    }, { threshold: 0.14 });
    document.querySelectorAll('.reveal').forEach(el=>observer.observe(el));

    // Animate skill bars when visible
    const bars = document.querySelectorAll('.fill');
    const barObserver = new IntersectionObserver((entries)=>{
      entries.forEach((entry)=>{
        if(entry.isIntersecting){
          const target = entry.target; const pct = +target.dataset.level || 0;
          target.style.transition = 'width 1.2s ease';
          requestAnimationFrame(()=> target.style.width = pct + '%');
          barObserver.unobserve(target);
        }
      })
    }, { threshold: 0.5 });
    bars.forEach(b=>barObserver.observe(b));

    // Smooth show/hide Back-to-top button
    const toTop = document.getElementById('toTop');
    window.addEventListener('scroll', ()=>{
      if (window.scrollY > 500) toTop.classList.add('show'); else toTop.classList.remove('show');
    });
    toTop.addEventListener('click', ()=> window.scrollTo({ top: 0, behavior: 'smooth' }));

    // Current year
    document.getElementById('year').textContent = new Date().getFullYear();
  </script>
</body>
</html>
