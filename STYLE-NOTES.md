# Juris Prudentia: style notes for building units

Static site for GitHub Pages: plain HTML, inline CSS and JS, relative links only, no build step.
Copy CSS and the shared script from an existing `unit-1/` topic page; these notes say what to keep consistent.

## File layout
- `index.html` (root): "All units" hub (built separately). Every unit page links to it as `../index.html`.
- `unit-N/index.html`: unit landing page. Title `Unit II · Juris Prudentia` etc. Uses `.home` layout (hero + `.chapters` list + `.how`).
- `unit-N/<topic>.html`: one page per syllabus topic, short kebab-case names (`sources.html`, `natural-law.html`).
- `unit-N/exam.html`: exam kit for the whole unit.
- Unit I pages: `definition`, `nature`, `scope`, `sources`, `natural-law`, `exam`.

## Header and nav (identical on every page of a unit)
```
<header class="site-head"><div class="site-head-in">
  <a class="brand" href="index.html"><span class="brand-mark" aria-hidden="true">JP</span><span class="brand-text">Juris Prudentia</span></a>
  <nav class="site-nav" aria-label="Chapters"><a href="../index.html">All units</a><a href="topic-a.html">Topic A</a>…<a href="exam.html">Exam kit</a></nav>
</div><div class="progress" aria-hidden="true"><span></span></div></header>
```
- "All units" first, then topics in syllabus order, "Exam kit" last. The current page gets `aria-current="page"`.
- Brand links to the unit landing (`index.html`), not the root hub.

## Topic page skeleton
1. `<head>`: charset, viewport (`viewport-fit=cover`), `<title>Topic · Juris Prudentia</title>`, description, Google Fonts link (Bricolage Grotesque / Instrument Sans / JetBrains Mono), one `<style>`: shared base CSS (first ~200 lines, identical everywhere) + page-specific component CSS.
2. Header (above), then `<main class="wrap"><div class="layout rise"><article class="prose">`.
3. `<p class="eyebrow">Chapter X of N · Topic</p>`, `<h1>`, `<p class="meta">About NN minutes · N interactive widgets · N-question check</p>`, `<p class="lead">` (concrete hook, often an Indian case), one framing `<p>`.
4. Sections: `<h2 id="slug" data-toc="Short label">` (the shared JS builds the right-hand "On this page" rail and anchors from these). `<h3>` for subsections.
5. Close: `<h2 id="check">Check yourself</h2>` + `<div class="widget" id="quiz">…</div>`, then `.done-box` with `<button class="btn" data-done="<topic-slug>">`, then `<nav class="pager">` (previous / next; first links to `index.html`, last topic links to `exam.html`).
6. `</article><aside class="toc">…<ol></ol></aside></div><footer class="foot">…</footer></main>`.
7. Shared `<script>` (JP.store, JP.swap, progress bar, TOC, `JP.quiz`, done toggle), then a page `<script>` IIFE with widget code and `JP.quiz(el, [{q,o:[4],a,why}])`.

Progress: `data-done="slug"` writes localStorage `jp-done-slug`; the unit landing reads it via `<span class="status" data-status="slug" hidden>` in each `.ch` card.

## Components (class names)
- Prose: `.lead`, `.big-idea` (one-line takeaway), `mark` (key sentence to memorise), `.latin`, `.term`, `.hand` (mnemonic).
- Callouts: `<aside class="callout [exam|trap|keep|note]"><p class="label">…</p><p>…</p></aside>`. Labels used: "Exam lens" (exam), "Common mix-up" (trap), "How to write it up" / "Check your edition" (keep), "Sidenote" (note), "Who this is for" / "Where this fits" (plain).
- Quotes: `<blockquote class="defq"><p>…</p><cite>…</cite></blockquote>`.
- Tables: `<div class="table-wrap"><table>`; colour dots `<span class="dot" style="--dot:var(--c1)">`.
- Cards: `.case` > `.case-card` (`.tag` with `--d`, `.cn` name, `.cy` year, `p`); `.contrast` (two cards, `.them` = dark); `.etym` (3 tiles, `.eq` dark); `.recap` (key/value list); `.tree-wrap > .tree` (CSS org chart).
- Widgets: `.widget` > `.w-head` (`.w-tag` "Try it"/"Explore"/"Compare", `.w-title`, `.w-hint`). Buttons `.btn`, `.btn.primary`, toggles via `aria-pressed` or `.on`. `.chip`, `.row`, `.steps` (dot stepper), `.quiz-foot` + `.score`.
- Palette tokens: `--ink`, `--ink-2..4`, `--surface`, `--bg`, `--tint`, `--line`, `--violet`, `--good`/`--warn`/`--bad` (+ `-soft`), categorical `--c1..--c6`.
- Exam kit: `.qlist` with `.qtag.long` / `.qtag.short`; `<details class="skel">` answer skeletons (`.body > ol`, `.tip`); flashcards `.fc` (data array `C = [[front, back, note]]`); `.plan` (four week tiles).

## Tone and depth
- Second person, warm tutor voice ("Here's…", "Let's…"); short paragraphs; no emoji.
- Exam-oriented for Indian LL.B.: name the jurist every time, give one-line criticisms, add the Indian position (Articles, Supreme Court cases with years).
- Each topic page: 6–9 `h2` sections, 2–3 interactive widgets, a 4–5 question quiz; roughly 50–70 KB.
- Footer: "Juris Prudentia · a study companion to Dr N.V. Paranjape, *Studies in Jurisprudence & Legal Theory*, Unit N…".
