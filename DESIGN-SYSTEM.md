# Portfolio Migration — Design System & Handoff

Goal: migrate every page of the portfolio to one minimal system. All pages link a single shared `style.css`. Keep all content; strip the decorative chrome.

## Files
- `style.css` — the system. Single source of truth for all styling. Every page links it.
- `index.html` — home (reference: see the minimal home build).
- `galaxy-guide.html` — case-study page (reference: see the minimal detail build).

## The one color rule
`--hl` (currently `#CCF23E`) is a **highlighter only**.
- Never use it as text color.
- Never use it as a filled block/card background.
- It appears statically on **one** number per case study (the headline metric), and on hover/active states (home project items, listing rows, active TOC item). That's it.
- To re-accent the whole site, change the single `--hl` value in `style.css`.

## Type & tokens
Source of truth is `style.css`. Summary: Helvetica Neue / Helvetica / Arial stack, black on white, hairline rules (`--line`), reading column `--measure` 660px, detail container `--max` 1080px. No webfonts, no pills, no blobs, no colored boxes.

## Component translation (old rich page → minimal)
Apply these when converting an existing page:

| Old (AI-kit) element            | Minimal replacement                                            |
|---------------------------------|----------------------------------------------------------------|
| Pill / badge eyebrow            | Plain uppercase letter-spaced text (`.eyebrow`)                |
| Filled stat card / color band   | Big black numbers, no fill (`.stats .stat .n`); highlight ONE  |
| Tinted callout box w/ color edge| Hairline left-indent block (`.callout`)                        |
| Bordered/hover cards (2-up)     | Two-column text divided by a top rule (`.two .col`)            |
| Colored table header + zebra    | Swiss table; header rule only; chosen cell = bold (`td.chosen`)|
| Process dots + accent circles   | Big numbers 01–05, hairline between (`.step .sn`)              |
| Decorative blobs / gradients    | Remove                                                         |
| Emoji in headings               | Remove                                                         |
| Colored section labels          | Grey/black labels (`.aside .lbl`); never colored text          |

## Page skeletons

### Home (`index.html`)
```html
<body class="home">
  <div class="top">
    <a href="index.html" class="name">Riley Baik</a>
    <div></div>
    <div class="links">
      <a href="LINKEDIN_URL" aria-label="LinkedIn"><svg viewBox="0 0 24 24"><path d="M4.98 3.5a2.5 2.5 0 1 1 0 5 2.5 2.5 0 0 1 0-5zM3 9h4v12H3zM9 9h3.8v1.7h.1c.5-1 1.8-2 3.7-2 4 0 4.7 2.6 4.7 6V21h-4v-5.3c0-1.3 0-2.9-1.8-2.9s-2 1.4-2 2.8V21H9z"/></svg></a>
      <a href="mailto:EMAIL" aria-label="Email"><svg viewBox="0 0 24 24"><path d="M3 5h18a1 1 0 0 1 1 1v12a1 1 0 0 1-1 1H3a1 1 0 0 1-1-1V6a1 1 0 0 1 1-1zm0 2v.4l9 5.6 9-5.6V7H3zm18 2.3-9 5.6-9-5.6V18h18z"/></svg></a>
    </div>
  </div>
  <div class="main-split">
    <div class="left">
      <h1>Riley Baik</h1>
      <p class="intro">Product Manager focusing on <span class="hl">AI/ML&#8209;powered</span> products.</p>
      <div class="bio-meta">Bothell, WA<br>Open to AI/ML PM roles</div>
    </div>
    <div class="right">
      <div class="group">
        <div class="cat">Work</div>
        <div>
          <div class="items">
            <a class="item" href="..."><span class="t">Title</span><span class="m">Company</span></a>
          </div>
          <a class="more" href="...">More →</a>
        </div>
      </div>
      <!-- repeat .group for Concepts, Build, Write -->
    </div>
  </div>
</body>
```

### Case study (`galaxy-guide.html` and all other detail pages)
```html
<body>
  <div class="top">
    <a href="index.html" class="name">Riley Baik</a>
    <nav class="nav-center">
      <a href="work.html">Work</a>
      <a href="proposals.html">Proposals</a>
      <a href="build.html">Build</a>
      <a href="writing.html">Writing</a>
    </nav>
    <div class="links">
      <a href="LINKEDIN_URL" aria-label="LinkedIn"><svg viewBox="0 0 24 24"><path d="M4.98 3.5a2.5 2.5 0 1 1 0 5 2.5 2.5 0 0 1 0-5zM3 9h4v12H3zM9 9h3.8v1.7h.1c.5-1 1.8-2 3.7-2 4 0 4.7 2.6 4.7 6V21h-4v-5.3c0-1.3 0-2.9-1.8-2.9s-2 1.4-2 2.8V21H9z"/></svg></a>
      <a href="mailto:EMAIL" aria-label="Email"><svg viewBox="0 0 24 24"><path d="M3 5h18a1 1 0 0 1 1 1v12a1 1 0 0 1-1 1H3a1 1 0 0 1-1-1V6a1 1 0 0 1 1-1zm0 2v.4l9 5.6 9-5.6V7H3zm18 2.3-9 5.6-9-5.6V18h18z"/></svg></a>
    </div>
  </div>
  <aside class="toc" id="toc">
    <div class="proj">Project Name</div>
    <ul>
      <li><a href="#overview">Overview</a></li>
      <li><a href="#problem">01 · The Problem</a></li>
      <!-- … -->
    </ul>
  </aside>
  <div class="wrap">
    <header class="hero">
      <div class="eyebrow">Work · Samsung.com</div>
      <h1>Project Name</h1>
      <p class="sub">One-line summary.</p>
      <div class="meta">
        <div><div class="l">Role</div><div class="v">…</div></div>
        <!-- … -->
      </div>
    </header>

    <section class="block" id="overview">
      <div class="grid">
        <div class="aside"><div class="lbl">Overview</div></div>
        <div class="main">
          <h2 class="t">Section headline.</h2>
          <div class="body"><p>…</p></div>
          <div class="stats">
            <div class="stat"><div class="n">300–500K</div><div class="sl">label</div></div>
            <div class="stat"><div class="n"><span class="hl">$300–500K</span></div><div class="sl">label</div></div>
          </div>
        </div>
      </div>
    </section>

    <section class="block" id="problem">
      <div class="grid">
        <div class="aside"><div class="num">01</div><div class="lbl">The Problem</div></div>
        <div class="main">
          <h2 class="t">…</h2>
          <div class="body"><p>…</p></div>
          <div class="callout"><span class="lead">Opportunity framing.</span> …</div>
          <div class="two">
            <div class="col"><div class="clabel">Label</div><p>…</p></div>
            <div class="col"><div class="clabel">Label</div><p>…</p></div>
          </div>
        </div>
      </div>
    </section>

    <!-- tables: .main.wide + <table> with td.chosen / td.no -->
    <!-- process: .steps > .step > .sn + (.st,.sb) -->

    <div class="foot">
      <a href="#">← Previous</a>
      <span class="copy">Riley Baik · PM Portfolio</span>
      <a href="#">Next →</a>
    </div>
  </div>
  <script>/* TOC scroll-spy — copy from galaxy-guide reference */</script>
</body>
```

### Listing page (Work / Concepts / Build / Write index)
```html
<body>
  <div class="top">…</div>
  <div class="wrap">
    <div class="list-head">
      <span class="eyebrow">Concepts</span>
      <h1>Product proposals for companies I'd want to build with.</h1>
    </div>
    <div class="rows">
      <a class="row" href="uber-eats-grocery.html">
        <div><div class="rt">Uber Eats Grocery</div><div class="rd">One-line summary.</div></div>
        <div class="rm">Concept · 2026</div>
      </a>
    </div>
    <div class="foot"><a href="index.html">← Home</a><span class="copy">Riley Baik · PM Portfolio</span><span></span></div>
  </div>
</body>
```

## TOC scroll-spy script (detail pages)
```html
<script>
  const toc = document.getElementById('toc');
  const hero = document.querySelector('.hero');
  const sections = document.querySelectorAll('section[id]');
  const links = document.querySelectorAll('.toc a');
  new IntersectionObserver(([e]) => { toc.classList.toggle('visible', !e.isIntersecting); }, { threshold: 0 }).observe(hero);
  const obs = new IntersectionObserver((entries) => {
    entries.forEach(entry => { if (entry.isIntersecting) {
      links.forEach(a => a.classList.remove('active'));
      const active = document.querySelector(`.toc a[href="#${entry.target.id}"]`);
      if (active) active.classList.add('active');
    }});
  }, { rootMargin: '-15% 0px -70% 0px' });
  sections.forEach(s => obs.observe(s));
  links.forEach(a => a.addEventListener('click', e => {
    e.preventDefault();
    const t = document.querySelector(a.getAttribute('href'));
    if (t) t.scrollIntoView({ behavior: 'smooth', block: 'start' });
  }));
</script>
```

## Pages to convert
- [x] Home → `index.html`
- [x] Galaxy Guide → `galaxy-guide.html` (reference)
- [ ] Uber Eats Grocery (Concept)
- [ ] Hybrid Search (Work)
- [ ] (list the rest)
- [ ] Listing pages: Work, Proposals, Build, Writing

## Paste-ready Claude Code prompt
> Migrate this portfolio repo to the minimal design system in `DESIGN-SYSTEM.md`.
> 1. Add `style.css` and link it from every page; remove all per-page inline `<style>` and any webfont/CDN links.
> 2. For each existing page, keep all content but restructure the markup to the skeletons and the component-translation table in `DESIGN-SYSTEM.md`. Keep existing filenames so shared links don't break.
> 3. Apply the shared header: wordmark links to `index.html`; LinkedIn/Email become the inline SVG icon links (replace text links); non-home pages get the centered nav (Work / Proposals / Build / Writing). Fill in my real LinkedIn URL and email.
> 4. Color: `--hl` is a highlighter only — one number per case study + hover/active states. Never colored text or filled blocks.
> 5. Remove section numbering (TOC and the `.aside .num`) but keep the Process step numbers (`.step .sn`).
> 6. Build the four listing pages (Work / Proposals / Build / Writing) and wire the home `More →` links and all cross-links.
> 7. Show me a diff per file before writing. Don't change copy except removing em dashes.

## Review checklist
- Every page links `style.css`; no inline styles or webfonts remain.
- `--hl` appears only as highlighter (one metric + hover/active). No colored text, no filled color blocks.
- Hairlines and whitespace carry hierarchy; no cards/pills/blobs.
- All `More →` and prev/next links resolve.
- Mobile: home stacks, tables/grids collapse, TOC hidden under 1280px.
