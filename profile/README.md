<div align="center">
  The intelligence layer for Industry 5.0 automation.
</div>

<blockquote style="text-align:center; margin-top:20px; font-size:1.2em; font-style:italic; padding:20px; border-left:4px solid #4CAF50; background:#f9f9f9;">
  Making Western manufacturing competitive through industrial intelligence.
</blockquote>

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Forgis — The brain of the factory</title>
<style>
  /* ============================================================
     Forgis brand typefaces (licensed, self-hosted).
     Loaded from the live site so this renders standalone.
     For production in your own codebase, point these at your local
     /_astro/fonts/ paths or your font CSS variables — the hashed
     filenames can change on each Astro rebuild.
     ============================================================ */
  @font-face {
    font-family: "At Hauss";
    font-weight: 400; font-style: normal; font-display: swap;
    src: url("https://www.forgis.com/_astro/fonts/b4851e16dd25198a.woff2") format("woff2");
  }
  @font-face {
    font-family: "At Hauss";
    font-weight: 400; font-style: italic; font-display: swap;
    src: url("https://www.forgis.com/_astro/fonts/1f25e9ef205c5e95.woff2") format("woff2");
  }
  @font-face {
    font-family: "PP Fraktion Mono";
    font-weight: 400; font-style: normal; font-display: swap;
    src: url("https://www.forgis.com/_astro/fonts/a69efcb473892502.woff2") format("woff2");
  }

  :root {
    --bg:        #dde0e0;   /* concrete grey */
    --ink:       #122128;   /* dark blue-black */
    --muted:     rgba(18,33,40,0.52);
    --line:      rgba(18,33,40,0.16);
    --accent:    #ff5a00;   /* forge orange */
    --accent-hi: #ff9030;   /* ember highlight */
    --sans: "At Hauss", Arial, sans-serif;
    --mono: "PP Fraktion Mono", ui-monospace, monospace;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    background: var(--bg);
    color: var(--ink);
    font-family: var(--sans);
    -webkit-font-smoothing: antialiased;
    position: relative;
    overflow-x: hidden;
  }

  /* forge glow bleeding from the top-right, like molten metal */
  body::before {
    content: "";
    position: fixed;
    top: -30vh; right: -20vw;
    width: 80vw; height: 80vh;
    background: radial-gradient(closest-side,
      rgba(255,90,0,0.30),
      rgba(255,144,48,0.12) 45%,
      transparent 72%);
    pointer-events: none;
    z-index: 0;
    filter: blur(8px);
  }
  /* faint film grain for industrial texture */
  body::after {
    content: "";
    position: fixed;
    inset: 0;
    pointer-events: none;
    z-index: 0;
    opacity: 0.05;
    background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='160' height='160'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='2'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
  }

  .wrap { position: relative; z-index: 2; max-width: 1180px; margin: 0 auto; padding: 0 32px; }

  /* ---- Hero ---- */
  .hero { text-align: center; padding: 86px 0 44px; }

  .logo {
    height: clamp(44px, 7vw, 78px);
    width: auto;
    color: var(--ink);
    opacity: 0;
    animation: rise 0.7s ease forwards;
  }

  .tagline {
    font-family: var(--sans);
    font-weight: 400;
    font-size: clamp(34px, 6vw, 68px);
    letter-spacing: -0.02em;
    line-height: 1.02;
    margin-top: 40px;
    opacity: 0;
    animation: rise 0.7s ease 0.12s forwards;
  }
  .tagline em { font-style: italic; color: var(--accent); }

  .stat {
    margin-top: 28px;
    font-family: var(--mono);
    font-size: 13.5px;
    letter-spacing: 0.13em;
    color: var(--muted);
    text-transform: uppercase;
    opacity: 0;
    animation: rise 0.7s ease 0.24s forwards;
  }
  .stat b { color: var(--accent); font-weight: 400; }
  .stat .bracket { color: rgba(18,33,40,0.3); }
  .stat .dot { margin: 0 12px; color: rgba(18,33,40,0.3); }

  .divider {
    height: 1px;
    background: var(--line);
    margin-top: 46px;
    transform: scaleX(0);
    transform-origin: center;
    animation: stretch 0.9s ease 0.3s forwards;
  }

  /* ---- Nav ---- */
  nav {
    display: flex; align-items: center; justify-content: space-between;
    flex-wrap: wrap; gap: 22px;
    padding: 24px 0 56px;
    font-family: var(--mono);
    opacity: 0;
    animation: rise 0.7s ease 0.42s forwards;
  }
  .nav-links { display: flex; gap: 30px; }
  .nav-links a {
    text-decoration: none; color: var(--muted);
    font-size: 13px; letter-spacing: 0.12em; text-transform: uppercase;
    transition: color 0.18s ease;
  }
  .nav-links a:hover { color: var(--ink); }

  .nav-right { display: flex; align-items: center; gap: 24px; }
  .social {
    display: flex; align-items: center; gap: 8px;
    color: var(--muted); font-size: 13px; font-variant-numeric: tabular-nums;
    text-decoration: none; transition: color 0.18s ease;
  }
  .social:hover { color: var(--ink); }
  .social svg { width: 17px; height: 17px; }

  .pill-wrap { position: relative; padding: 7px; }
  .pill {
    display: inline-block;
    background: var(--accent); color: #fff; border: none; border-radius: 2px;
    padding: 11px 24px;
    font-family: var(--mono); font-size: 12.5px; letter-spacing: 0.12em;
    text-transform: uppercase; text-decoration: none; cursor: pointer;
    transition: background 0.18s ease, transform 0.18s ease;
  }
  .pill:hover { background: #ff6a16; transform: translateY(-1px); }
  .pill-wrap::before, .pill-wrap::after,
  .pill-wrap span::before, .pill-wrap span::after {
    content: ""; position: absolute; width: 8px; height: 8px;
    border-color: rgba(18,33,40,0.35); border-style: solid;
  }
  .pill-wrap::before { top: 0; left: 0; border-width: 1.5px 0 0 1.5px; }
  .pill-wrap::after  { top: 0; right: 0; border-width: 1.5px 1.5px 0 0; }
  .pill-wrap span::before { bottom: 0; left: 0; border-width: 0 0 1.5px 1.5px; }
  .pill-wrap span::after  { bottom: 0; right: 0; border-width: 0 1.5px 1.5px 0; }

  @keyframes rise { from { opacity: 0; transform: translateY(14px); } to { opacity: 1; transform: translateY(0); } }
  @keyframes stretch { to { transform: scaleX(1); } }

  @media (max-width: 640px) {
    nav { justify-content: center; }
    .hero { padding: 56px 0 36px; }
  }
</style>
</head>
<body>

  <div class="wrap">
    <header class="hero">
      <!-- Real Forgis logotype -->
      <svg class="logo" viewBox="0 0 102 26" role="img" aria-label="Forgis" xmlns="http://www.w3.org/2000/svg">
        <path fill="currentColor" d="M71.47 6.78c2.02 0 3.85.96 4.78 2.54h.11V7.16c0-.16.08-.25.25-.25h1.97c.14 0 .22.08.22.25v15.58c0 2.1-1.15 3.25-3.25 3.25H68.2c-.14 0-.25-.08-.25-.25v-1.56c0-.14.11-.22.25-.22h8.06v-5.6h-.11c-.98 1.61-2.73 2.57-4.67 2.57-3.72 0-6.12-2.79-6.12-7.11s2.41-7.05 6.12-7.05ZM2.48 16.75c4.73-3.99 11.72-3.97 16.42.07.22.19.25.52.06.75-.41.49-.86.95-1.35 1.36-.22.18-.54.16-.75-.04l-4.74-4.73v6.63c0 .32-.26.57-.57.57h-1.8c-.32 0-.57-.26-.57-.58v-6.63l-4.67 4.67a.58.58 0 0 1-.81 0l-1.24-1.25a.546.546 0 0 1 .03-.81Zm89.21-9.97c3.01 0 4.84 1.42 5.14 3.88.03.19-.05.27-.19.27h-2.02c-.16 0-.22-.11-.25-.22-.3-1.37-1.12-1.97-2.68-1.97s-2.46.68-2.46 1.89c0 1.04.49 1.61 2.21 1.94l1.78.33c3.06.57 3.96 1.64 3.96 3.94 0 2.62-1.86 4.1-5.14 4.1s-5.33-1.5-5.63-4.24c-.03-.19.08-.27.22-.27h2c.16 0 .22.08.25.22.3 1.61 1.28 2.32 3.17 2.32 1.61 0 2.65-.77 2.65-2 0-1.09-.6-1.59-2.35-1.91l-1.64-.3c-2.76-.52-3.99-1.72-3.99-3.99 0-2.41 1.94-3.99 4.97-3.99m-43.38 0c4.1 0 6.89 2.87 6.89 7.11s-.08.25-.22.25h-2.08c-.16 0-.25-.08-.25-.25V10.28c0-2.19 1.18-3.36 3.36-3.36h4.13ZM40.35 1.67c.14 0 .25.08.25.25V3.7c0 .14-.11.22-.25.22h-9.24v6.34h8.69c.14 0 .25.11.25.25v1.78c0 .14-.11.25-.25.25h-8.69v8.04c0 .16-.08.25-.22.25h-2.16c-.16 0-.25-.08-.25-.25V1.92c0-.16.08-.25.25-.25zm43.72 5.25c.14 0 .22.08.22.25v13.4c0 .16-.08.25-.22.25h-2.08c-.16 0-.25-.08-.25-.25V7.16c0-.16.08-.25.25-.25h2.08ZM48.31 8.86c-2.65 0-4.26 1.91-4.26 5.03s1.61 4.98 4.26 4.98 4.29-1.89 4.29-4.98-1.64-5.03-4.29-5.03m23.84 0c-2.6 0-4.21 1.89-4.21 4.98s1.61 5.03 4.21 5.03 4.21-1.94 4.21-5.03-1.61-4.98-4.21-4.98M11.9.44c.05-.29.33-.48.62-.43.64.11 1.25.28 1.85.49.27.1.41.39.34.67L13 7.56l5.75-3.32a.56.56 0 0 1 .73.15c.38.53.7 1.09.98 1.68.12.26.02.57-.23.71l-5.76 3.32 6.45 1.73c.28.07.46.34.41.62-.11.64-.27 1.26-.49 1.86-.1.28-.4.42-.68.32-2.85-1-5.23-2.96-6.76-5.6A12.54 12.54 0 0 1 11.91.44ZM8.78 0c.29-.05.57.14.62.43.54 2.95.02 5.96-1.49 8.58-1.52 2.64-3.88 4.6-6.73 5.6-.28.1-.58-.04-.68-.32-.21-.6-.3-1.86-.05-.28.13-.55.41-.62l6.43-1.72-5.75-3.3a.55.55 0 0 1-.23-.71c.28-.59.6-1.16.98-1.68a.56.56 0 0 1 .73-.15l5.73 3.3-1.71-6.38C6.54.89 6.68.6 6.95.5 7.54.28 8.16.12 8.8 0Zm90.79 1.22c1.34 0 2.43 1.09 2.43 2.43s-1.09 2.43-2.43 2.43-2.43-1.09-2.43-2.43 1.09-2.43 2.43-2.43m0 .44c-1.1 0-1.97.9-1.97 1.99a1.97 1.97 0 1 0 3.94 0c0-1.08-.87-1.99-1.97-1.99m.22.62c.57 0 .87.32.87.74 0 .4-.24.63-.55.68.36 0 .52.13.52.53v.73h-.52v-.7c0-.21-.1-.31-.35-.31h-.65v1h-.53V2.28zm-15.45-1.1c.14 0 .22.11.22.25v2.6c0 .14-.08.25-.22.25h-2.62c-.14 0-.22-.11-.22-.25V1.42c0-.14.08-.25.22-.25h2.62Zm14.77 2.35h.52c.32 0 .5-.13.5-.4 0-.31-.18-.4-.5-.4h-.52v.81Z"/>
      </svg>

      <h1 class="tagline">The brain of the<br><em>factory</em></h1>

      <p class="stat">
        <span class="bracket">[</span> <b>5/5</b> ICML 2026 ACCEPTANCES <span class="bracket">]</span>
        <span class="dot">/</span>
        <span class="bracket">[</span> <b>$4.5M</b> RAISED IN 36HR <span class="bracket">]</span>
      </p>

      <div class="divider"></div>
    </header>

    <nav>
      <div class="nav-links">
        <a href="https://www.forgis.com/#papers">RESEARCH</a>
        <a href="https://www.forgis.com/#the-making-kind">MANIFESTO</a>
      </div>

      <div class="nav-right">
        <a class="social" href="https://github.com/Forgis-Labs" title="GitHub">
          <svg viewBox="0 0 24 24" fill="currentColor"><path d="M12 .5C5.7.5.5 5.7.5 12c0 5.1 3.3 9.4 7.9 10.9.6.1.8-.2.8-.5v-2c-3.2.7-3.9-1.4-3.9-1.4-.5-1.3-1.3-1.7-1.3-1.7-1.1-.7.1-.7.1-.7 1.2.1 1.8 1.2 1.8 1.2 1 1.8 2.7 1.3 3.4 1 .1-.8.4-1.3.7-1.6-2.6-.3-5.3-1.3-5.3-5.7 0-1.3.5-2.3 1.2-3.1-.1-.3-.5-1.5.1-3.1 0 0 1-.3 3.3 1.2 1-.3 2-.4 3-.4s2 .1 3 .4c2.3-1.5 3.3-1.2 3.3-1.2.6 1.6.2 2.8.1 3.1.8.8 1.2 1.8 1.2 3.1 0 4.4-2.7 5.4-5.3 5.7.4.4.8 1.1.8 2.2v3.3c0 .3.2.6.8.5 4.6-1.5 7.9-5.8 7.9-10.9C23.5 5.7 18.3.5 12 .5z"/></svg>
          <span>—</span>
        </a>
        <a class="social" href="https://www.linkedin.com/company/forgisai" title="LinkedIn">
          <svg viewBox="0 0 24 24" fill="currentColor"><path d="M20.5 2h-17A1.5 1.5 0 0 0 2 3.5v17A1.5 1.5 0 0 0 3.5 22h17a1.5 1.5 0 0 0 1.5-1.5v-17A1.5 1.5 0 0 0 20.5 2zM8 19H5v-9h3zM6.5 8.3a1.7 1.7 0 1 1 0-3.4 1.7 1.7 0 0 1 0 3.4zM19 19h-3v-4.7c0-1.1 0-2.5-1.5-2.5S12.8 13 12.8 14.2V19h-3v-9h2.9v1.2h.1a3.2 3.2 0 0 1 2.9-1.6c3.1 0 3.7 2 3.7 4.7z"/></svg>
          <span>—</span>
        </a>
        <a class="social" href="https://x.com/ForgisX" title="X">
          <svg viewBox="0 0 24 24" fill="currentColor"><path d="M18.9 1.5h3.7l-8 9.2 9.4 12.4h-7.4l-5.8-7.6-6.6 7.6H.5l8.6-9.8L0 1.5h7.6l5.2 6.9zm-1.3 19.8h2L6.5 3.6H4.4z"/></svg>
          <span>—</span>
        </a>
        <div class="pill-wrap"><span></span><a class="pill" href="https://join.slack.com/t/forgis/shared_invite/zt-3zc0shfro-_tFYCnf_v_kN8HL1AfTo0Q">JOIN SLACK</a></div>
      </div>
    </nav>
  </div>
</body>
</html>

## The Problem Today

- **Unused data**: Factories stream sensor data every millisecond but less than 1% ever drives a decision.
- **Vanishing expertise**: Veteran operators read a machine by feel, but that intuition leaves with them as the workforce retires.
- **Lost output**: Median OEE sits at 60%, far below the 85% world-class benchmark, while unplanned downtime erodes revenue.

The signals are there. The intelligence isn't.

## The Solution

**Forgis is the intelligent layer for the real world**, AI-native orchestration infrastructure that brings physical intelligence into hardware. Causal AI agents run on the edge as digital engineers: they learn from data, predict failures, optimize performance in real time, and guide operators to act before downtime occurs. From one unified interface, Forgis connects machines, information, and logic - turning disconnected automation into the brain of the factory.

The goal is Industry 5.0: plug-and-play factories that are adaptive, collaborative, and self-optimizing. Orders flow from digital marketplaces straight into the line, agents reconfigure machines on demand, and strategy becomes execution. Humans conduct; the factory orchestrates itself below.

### Two Verticals

- **🤖 Robotics**: AI-native configuration, validation, and control of robotic cells — agents that program, calibrate, and adapt robots in real time, collapsing integration time and removing vendor lock-in.
- **⚙️ Process Optimization**: Causal agents that monitor production lines end-to-end, predict failures weeks ahead, trace quality defects to their root cause, and tune parameters for throughput and energy.


## 🔬 Research

Our components are backed by peer-reviewed work — **5 ICML 2026 workshop acceptances and 3 NeurIPS submissions** — with data, code, and models released fully open-source, all produced in 5 months.

- **[HEPA](https://www.forgis.com/papers/hepa.html)** *(Spotlight, FMSD @ ICML)* — the encoder: a JEPA-based foundation model architecture, validated against SOTA on 10 benchmarks; scaling to HEPA-Base 200M in Stage 1.
- **[FactoryNet](https://www.forgis.com/papers/factorynet.html)** *(FMSD + AI4Physics @ ICML)* — the pretraining data: a large-scale industrial dataset of 1B+ sensor measurements seeding the Stage 1 corpus.
- **[FactoryBench](https://www.forgis.com/papers/factorybench.html)** — the evaluation framework: a benchmark for industrial machine understanding.
- **[TEMPO](https://www.forgis.com/papers/tempo.html)** *(FMSD @ ICML)* — the language grounding: semantic grounding via discrete time-series tokenization; a Stage 2 semantic prior.
- **[RASA](https://www.forgis.com/papers/rasa.html)** *(GFM @ ICML)* — the knowledge-graph theory: a structural inductive bias for reasoning over knowledge graphs, grounding the Stage 2 semantic priors.

👉 Code & models: [github.com/Forgis-Labs](https://github.com/Forgis-Labs)


## 🤝 Join Our Slack

We're opening access to **engineers, integrators, and manufacturers** who want to shape the future of automation.

👉 [Join our Slack](https://join.slack.com/t/xelerit-robotics/shared_invite/zt-3bu5mhaau-PnUPklHcHZ4kfPPUIkQK9w)


## 📄 License

Forgis © 2025 — All rights reserved.
