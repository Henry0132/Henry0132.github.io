# Academic Homepage Redesign (Classic Academic) Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Replace the current single-column academic homepage with a two-column Classic Academic (Jon Barron style) layout, add the accepted NeurIPS 2026 paper, and keep the URL `https://henry0132.github.io` unchanged.

**Architecture:** Pure static HTML + CSS. Rewrite `index.html` and `style.css` in place; reuse the existing `photo.jpg` and the existing git remote (`Henry0132.github.io`). No JavaScript, no build step, no new dependencies.

**Tech Stack:** HTML5, CSS3 (flexbox + media query), git / GitHub Pages.

**Spec:** `docs/superpowers/specs/2026-09-25-academic-homepage-template-design.md`

---

## File Structure

- Modify: `style.css` — full rewrite, Classic Academic two-column styles.
- Modify: `index.html` — full rewrite, sidebar + main column, all content.
- Unchanged: `photo.jpg`, `.gitignore`, `docs/`.

No new files. Footer stays outside the flex layout so it centers on the page.

### Task 1: Rewrite `style.css`

**Files:**
- Modify: `style.css` (full replacement)

- [ ] **Step 1: Replace the entire contents of `style.css` with:**

```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  line-height: 1.6;
  color: #333;
  background-color: #fff;
}

.layout {
  max-width: 1000px;
  margin: 0 auto;
  padding: 48px 24px;
  display: flex;
  gap: 56px;
  align-items: flex-start;
}

/* ---- Sidebar ---- */
.sidebar {
  flex: 0 0 230px;
  position: sticky;
  top: 48px;
  text-align: center;
}

.avatar {
  width: 160px;
  height: 160px;
  border-radius: 50%;
  object-fit: cover;
  margin-bottom: 18px;
}

h1 {
  font-size: 1.45em;
  font-weight: 600;
  color: #1a1a1a;
  line-height: 1.3;
}

.affiliation {
  font-size: 0.88em;
  color: #666;
  margin-top: 8px;
  line-height: 1.5;
}

.sidebar-links {
  list-style: none;
  padding-left: 0;
  margin-top: 16px;
  font-size: 0.82em;
  line-height: 1.9;
}

.sidebar-links li {
  margin-bottom: 0;
  word-break: break-all;
}

/* ---- Main column ---- */
.main {
  flex: 1;
  min-width: 0;
}

section {
  margin-bottom: 38px;
}

h2 {
  font-size: 1.25em;
  font-weight: 600;
  color: #1a1a1a;
  border-bottom: 2px solid #eee;
  padding-bottom: 6px;
  margin-bottom: 16px;
}

a {
  color: #2a7ae2;
  text-decoration: none;
}

a:hover {
  text-decoration: underline;
}

ul {
  padding-left: 20px;
}

li {
  margin-bottom: 6px;
}

/* ---- News ---- */
.news-list {
  list-style: none;
  padding-left: 0;
}

.news-list li {
  display: flex;
  gap: 12px;
  margin-bottom: 6px;
}

.news-date {
  color: #888;
  font-family: monospace;
  font-size: 0.9em;
  white-space: nowrap;
}

/* ---- Publications ---- */
.pub {
  margin-bottom: 20px;
}

.pub-title {
  font-weight: 600;
  font-size: 1.02em;
}

.pub-authors {
  color: #555;
  font-size: 0.95em;
}

.pub-venue {
  color: #888;
  font-size: 0.9em;
}

.pub-links {
  font-size: 0.9em;
  margin-top: 3px;
}

.pub-links a {
  margin-right: 10px;
  font-family: monospace;
}

/* ---- Education ---- */
.entry {
  display: flex;
  justify-content: space-between;
  align-items: baseline;
  gap: 12px;
  margin-bottom: 14px;
}

.school {
  color: #666;
}

.dates {
  color: #888;
  font-size: 0.9em;
  white-space: nowrap;
}

/* ---- Awards ---- */
.award-period {
  font-weight: 600;
  font-size: 0.95em;
  color: #666;
  margin-top: 12px;
  margin-bottom: 4px;
}

/* ---- Footer ---- */
footer {
  text-align: center;
  color: #aaa;
  font-size: 0.85em;
  padding: 0 24px 40px;
}

/* ---- Mobile ---- */
@media (max-width: 768px) {
  .layout {
    flex-direction: column;
    gap: 32px;
    padding: 32px 20px;
  }

  .sidebar {
    flex: none;
    width: 100%;
    position: static;
  }

  .entry {
    flex-direction: column;
    gap: 0;
  }

  .news-list li {
    flex-direction: column;
    gap: 0;
  }
}
```

- [ ] **Step 2: Verify CSS is syntactically balanced**

Run:
```powershell
$css = Get-Content -Raw -LiteralPath "style.css"
$open = ([regex]::Matches($css, '\{')).Count
$close = ([regex]::Matches($css, '\}')).Count
if ($open -eq $close) { "PASS: braces balanced ($open)" } else { "FAIL: $open open vs $close close" }
if ($css -match '@media\s*\(max-width:\s*768px\)') { "PASS: mobile media query present" } else { "FAIL: media query missing" }
if ($css -match '\.sidebar[\s\S]*?position:\s*sticky') { "PASS: sticky sidebar present" } else { "FAIL: sticky sidebar missing" }
```
Expected: three PASS lines.

- [ ] **Step 3: Commit**

```powershell
git add style.css
git commit -m "restyle: Classic Academic two-column layout"
```

### Task 2: Rewrite `index.html`

**Files:**
- Modify: `index.html` (full replacement)

- [ ] **Step 1: Replace the entire contents of `index.html` with:**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Hengrui Zhang — Homepage</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <div class="layout">
    <aside class="sidebar">
      <img src="photo.jpg" alt="Hengrui Zhang" class="avatar" onerror="this.style.display='none'">
      <h1>Hengrui Zhang</h1>
      <p class="affiliation">
        Ph.D. Student<br>
        <a href="https://www.cumt.edu.cn/">China University of Mining and Technology</a>
      </p>
      <ul class="sidebar-links">
        <li><a href="mailto:hengruizhang@cumt.edu.cn">hengruizhang@cumt.edu.cn</a></li>
        <li><a href="mailto:hengruizhang0132@gmail.com">hengruizhang0132@gmail.com</a></li>
        <li><a href="https://github.com/Henry0132">GitHub</a></li>
        <li><a href="https://scholar.google.com.hk/citations?user=PFxa-9YAAAAJ&hl=zh-CN">Google Scholar</a></li>
      </ul>
    </aside>

    <main class="main">
      <section>
        <h2>About</h2>
        <p>
          I am a first-year Ph.D. student at the School of Information and Control Engineering,
          <a href="https://www.cumt.edu.cn/">China University of Mining and Technology</a> (CUMT), born on March 2, 2001.
          My research focuses on offline reinforcement learning, goal-conditioned reinforcement learning, and generative models.
          I am advised by <a href="https://siee.cumt.edu.cn/info/1012/1025.htm">Prof. Xuesong Wang</a>.
        </p>
      </section>

      <section>
        <h2>Research Interests</h2>
        <ul>
          <li>Offline Reinforcement Learning</li>
          <li>Goal-Conditioned Reinforcement Learning</li>
          <li>Generative Models</li>
        </ul>
      </section>

      <section>
        <h2>News</h2>
        <ul class="news-list">
          <li><span class="news-date">[2026]</span><span>One paper accepted at NeurIPS 2026 as Poster.</span></li>
        </ul>
      </section>

      <section>
        <h2>Publications</h2>

        <div class="pub">
          <p class="pub-title">Diffusion Subgoal Planning for Long-Horizon Offline Goal-Conditioned Reinforcement Learning</p>
          <p class="pub-authors"><strong>Hengrui Zhang</strong>, Yuhu Cheng, C. L. Philip Chen, Xuesong Wang</p>
          <p class="pub-venue"><em>Conference on Neural Information Processing Systems (NeurIPS), 2026 (Poster)</em></p>
        </div>

        <div class="pub">
          <p class="pub-title">Return-Critic: Bridging Goal Discrepancy for Efficient Visual Reinforcement Learning</p>
          <p class="pub-authors">Ruyi Lu, Xuesong Wang, <strong>Hengrui Zhang</strong>, Yuhu Cheng</p>
          <p class="pub-venue"><em>International Conference on Machine Learning (ICML), 2026</em></p>
          <p class="pub-links">
            <a href="#">[paper]</a> <a href="#">[code]</a> <a href="#">[bibtex]</a>
          </p>
        </div>

        <div class="pub">
          <p class="pub-title">PCDT: Pessimistic Critic Decision Transformer for Offline Reinforcement Learning</p>
          <p class="pub-authors">Xuesong Wang, <strong>Hengrui Zhang</strong>, Jiazhi Zhang, C. L. Philip Chen, Yuhu Cheng</p>
          <p class="pub-venue"><em>IEEE Transactions on Systems, Man, and Cybernetics: Systems, 2025, 55(10): 7247–7258</em></p>
          <p class="pub-links">
            <a href="https://doi.org/10.1109/TSMC.2025.3583392">[DOI]</a>
          </p>
        </div>

        <div class="pub">
          <p class="pub-title">Visual Reinforcement Learning Based on Multiview Optimization Aggregation</p>
          <p class="pub-authors">Xuesong Wang, Ruyi Lu, <strong>Hengrui Zhang</strong>, Yuhu Cheng</p>
          <p class="pub-venue"><em>IEEE Transactions on Cognitive and Developmental Systems, 2025, 17(4): 1011–1021</em></p>
          <p class="pub-links">
            <a href="https://doi.org/10.1109/TCDS.2025.3540115">[DOI]</a>
          </p>
        </div>

        <div class="pub">
          <p class="pub-title">Diffusion Policy Distillation for Offline Reinforcement Learning</p>
          <p class="pub-authors">Jiazhi Zhang, Yuhu Cheng, C. L. Philip Chen, <strong>Hengrui Zhang</strong>, Xuesong Wang</p>
          <p class="pub-venue"><em>Neural Networks, 2025, 190: 107694</em></p>
          <p class="pub-links">
            <a href="https://doi.org/10.1016/j.neunet.2025.107694">[DOI]</a>
          </p>
        </div>

        <div class="pub">
          <p class="pub-title">Offline Reinforcement Learning Based on Advantage-Constrained Diffusion Policy</p>
          <p class="pub-authors">Xuesong Wang, <strong>Hengrui Zhang</strong>, Jiazhi Zhang, Yuhu Cheng</p>
          <p class="pub-venue"><em>Control and Decision, 2025, 40(06): 1903–1912</em></p>
          <p class="pub-links">
            <a href="https://doi.org/10.13195/j.kzyjc.2024.0618">[DOI]</a>
          </p>
        </div>
      </section>

      <section>
        <h2>Education</h2>
        <div class="entry">
          <div class="entry-left">
            <strong>Ph.D. in Control Science and Engineering</strong><br>
            <span class="school"><a href="https://www.cumt.edu.cn/">China University of Mining and Technology</a></span>
          </div>
          <div class="entry-right">
            <span class="dates">2025 — Present</span>
          </div>
        </div>
        <div class="entry">
          <div class="entry-left">
            <strong>M.Sc. in Control Science and Engineering</strong><br>
            <span class="school"><a href="https://www.cumt.edu.cn/">China University of Mining and Technology</a></span>
          </div>
          <div class="entry-right">
            <span class="dates">2023 — 2025</span>
          </div>
        </div>
        <div class="entry">
          <div class="entry-left">
            <strong>B.Sc. in Internet of Things Engineering</strong><br>
            <span class="school"><a href="https://www.ycit.edu.cn/en/">Yancheng Institute of Technology</a></span>
          </div>
          <div class="entry-right">
            <span class="dates">2019 — 2023</span>
          </div>
        </div>
      </section>

      <section>
        <h2>Honors &amp; Awards</h2>

        <p class="award-period">Ph.D.</p>
        <ul>
          <li>First-Class Entrance Scholarship</li>
        </ul>

        <p class="award-period">M.Sc.</p>
        <ul>
          <li>Second-Class Entrance Scholarship</li>
          <li>Second-Class Academic Scholarship</li>
        </ul>

        <p class="award-period">B.Sc.</p>
        <ul>
          <li>National Scholarship</li>
          <li>National Endeavor Scholarship</li>
          <li>Yancheng "Yellow Sea Pearl" Scholarship</li>
          <li>First-Class Academic Scholarship ×8</li>
          <li>National Second Prize, 17th "Challenge Cup"</li>
          <li>National Third Prize, China College Student Computer Design Competition</li>
          <li>National Second Prize, China College Student Computer Design Competition (Preliminary)</li>
        </ul>
      </section>
    </main>
  </div>

  <footer>
    <p>Last updated: September 2026</p>
  </footer>
</body>
</html>
```

- [ ] **Step 2: Verify all required content is present**

Run:
```powershell
$html = Get-Content -Raw -LiteralPath "index.html"
$needles = @(
  "Hengrui Zhang",
  "Diffusion Subgoal Planning for Long-Horizon Offline Goal-Conditioned Reinforcement Learning",
  "NeurIPS), 2026 (Poster)",
  "One paper accepted at NeurIPS 2026 as Poster.",
  "Return-Critic: Bridging Goal Discrepancy for Efficient Visual Reinforcement Learning",
  "PCDT: Pessimistic Critic Decision Transformer for Offline Reinforcement Learning",
  "Visual Reinforcement Learning Based on Multiview Optimization Aggregation",
  "Diffusion Policy Distillation for Offline Reinforcement Learning",
  "Offline Reinforcement Learning Based on Advantage-Constrained Diffusion Policy",
  "Ph.D. in Control Science and Engineering",
  "M.Sc. in Control Science and Engineering",
  "B.Sc. in Internet of Things Engineering",
  "First-Class Entrance Scholarship",
  "Second-Class Entrance Scholarship",
  "Second-Class Academic Scholarship",
  "National Scholarship",
  "National Endeavor Scholarship",
  "First-Class Academic Scholarship ×8",
  "National Second Prize, 17th \"Challenge Cup\"",
  "National Third Prize, China College Student Computer Design Competition",
  "National Second Prize, China College Student Computer Design Competition (Preliminary)",
  "hengruizhang@cumt.edu.cn",
  "hengruizhang0132@gmail.com",
  "https://github.com/Henry0132",
  "scholar.google.com.hk/citations?user=PFxa-9YAAAAJ",
  "https://doi.org/10.1109/TSMC.2025.3583392",
  "https://doi.org/10.1109/TCDS.2025.3540115",
  "https://doi.org/10.1016/j.neunet.2025.107694",
  "https://doi.org/10.13195/j.kzyjc.2024.0618",
  "https://siee.cumt.edu.cn/info/1012/1025.htm",
  "https://www.ycit.edu.cn/en/",
  "Research Interests",
  "Honors &amp; Awards",
  "Last updated: September 2026"
)
$missing = @($needles | Where-Object { $html -notmatch [regex]::Escape($_) })
if ($missing.Count -eq 0) { "PASS: all content present" } else { "FAIL: missing -> $($missing -join ' | ')" }
$pubCount = ([regex]::Matches($html, 'class="pub"')).Count
if ($pubCount -eq 6) { "PASS: 6 publications" } else { "FAIL: found $pubCount publications" }
```
Expected: `PASS: all content present` and `PASS: 6 publications`.

- [ ] **Step 3: Verify HTML structure and links**

Run:
```powershell
$html = Get-Content -Raw -LiteralPath "index.html"
$h2 = ([regex]::Matches($html, '<h2>')).Count
$links = [regex]::Matches($html, 'href="([^"]*)"') | ForEach-Object { $_.Groups[1].Value }
$bad = @($links | Where-Object { $_ -ne "#" -and $_ -notmatch '^(https?://|mailto:)' })
if ($h2 -eq 6) { "PASS: 6 sections" } else { "FAIL: $h2 sections" }
if ($bad.Count -eq 0) { "PASS: all $($links.Count) links valid ($(($links | Where-Object { $_ -ne '#' }).Count) real, $(($links | Where-Object { $_ -eq '#' }).Count) placeholders)" } else { "FAIL: $($bad -join ' | ')" }
[string]::Join("`n", $links)
```
Expected: `PASS: 6 sections`, all links valid; printed list must contain the 4 DOI links, 4 CUMT links (sidebar + About + 2 in Education), 1 advisor link, 1 YCIT link, 1 GitHub, 1 Scholar, 2 mailto, 3 `#` placeholders.

- [ ] **Step 4: Commit**

```powershell
git add index.html
git commit -m "rebuild homepage with Classic Academic template and NeurIPS 2026 paper"
```

### Task 3: Local visual verification

**Files:** none modified (verification only)

- [ ] **Step 1: Open the page in the default browser**

Run:
```powershell
Start-Process "$PWD\index.html"
```
Expected: browser opens the local file. Ask the user to confirm: two columns on desktop, photo and links on the left, 6 publications, News section visible, footer present.

- [ ] **Step 2: Check narrow-viewport behavior**

Ask the user to narrow the browser window below ~768 px width (or use DevTools device mode).
Expected: sidebar stacks on top, entries collapse to one column, no horizontal scrolling.

- [ ] **Step 3: Fix any visual issues found, then re-commit if changed**

```powershell
git add -A
git commit -m "fix: address visual issues from local preview"
```
(Skip this commit if no changes were needed.)

### Task 4: Deploy and verify live site

**Files:** none modified (deployment only)

- [ ] **Step 1: Push to GitHub**

Run:
```powershell
git push
```
Expected: push succeeds to `origin/main`.

- [ ] **Step 2: Wait for GitHub Pages deployment, then verify live content**

Run (wait ~90 seconds first; Pages deploy is async):
```powershell
Start-Sleep -Seconds 90
$live = (Invoke-WebRequest -Uri "https://henry0132.github.io" -UseBasicParsing -TimeoutSec 30).Content
$checks = @("Diffusion Subgoal Planning", "NeurIPS 2026", "class=`"sidebar`"", "Honors")
$missing = @($checks | Where-Object { $live -notmatch [regex]::Escape($_) })
if ($missing.Count -eq 0) { "PASS: live site updated" } else { "FAIL: live site missing $($missing -join ' | ') (may need more time or hard refresh)" }
```
Expected: `PASS: live site updated`. If FAIL, wait another 60 s and retry once.

- [ ] **Step 3: Report result to user**

Tell the user the new page is live at `https://henry0132.github.io`, and note that a hard refresh (`Ctrl+Shift+R`) may be needed to bypass browser cache.

---

## Self-Review

**Spec coverage:**
- Two-column layout, sticky sidebar, mobile single column → Task 1 (`.layout`, `.sidebar`, media query).
- Sidebar: photo, name, affiliation, both emails, GitHub, Scholar → Task 2 Step 1.
- About / Research Interests / News / Publications (6) / Education / Awards → Task 2 Step 1; asserted in Step 2.
- News entry `[2026] One paper accepted at NeurIPS 2026 as Poster.` → Task 2 Step 1/2.
- Footer "Last updated: September 2026" → Task 2 Step 1/2.
- URL unchanged, push to same repo → Task 4.
- Pure HTML/CSS, no build → no dependency tasks anywhere.

**Placeholder scan:** No TBD/TODO. All code and commands are complete. The only intentional placeholders are the pre-existing `#` links on the ICML paper, preserved from the old site at the user's request.

**Type consistency:** CSS class names used in `index.html` (`layout`, `sidebar`, `avatar`, `affiliation`, `sidebar-links`, `main`, `news-list`, `news-date`, `pub`, `pub-title`, `pub-authors`, `pub-venue`, `pub-links`, `entry`, `school`, `dates`, `award-period`) all exist in the `style.css` from Task 1. Section count expectation (6) matches the 6 `<section>` blocks: About, Research Interests, News, Publications, Education, Honors & Awards.
