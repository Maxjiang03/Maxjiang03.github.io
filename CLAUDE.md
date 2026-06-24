# CLAUDE.md

> Project context file for Claude Code. **Read this before making any change to the repository.**
> It defines the goals, conventions, and guardrails for this site. When in doubt, prefer the rules
> here over generic defaults. The single source of truth for all content is **Appendix A**.

---

## 1. Project Overview & Goals

Personal academic homepage for **Yixian Jiang**, built to support **PhD applications,
faculty outreach (cold emails), and scholarly-identity presentation**. This is a *content site*, not
a frontend showcase - clarity, accuracy, and information density matter more than visual novelty.

- **Primary audience**: PhD admissions committees and prospective advisors in security and AI.
- **Research positioning (the site's through-line)**: *Secure and Trustworthy Agentic AI Systems,
  LLM Security, AI-enabled Cyber Defence, IoT/ICS Security.*

**v1 success criteria**
- Loads fast; reads well on both mobile and desktop.
- A visitor grasps who Yixian is, the research direction, and the concrete evidence
  (publication, projects, CV) within ~30 seconds.
- Every fact is verifiable and accurately labeled.

**Non-goals for v1** (defer to a later personalized rebuild): blog/posts, talks/teaching pages,
animations, custom JS frameworks, visual experimentation.

---

## 2. Tech Stack

- **Template**: AcademicPages (a fork of the Minimal Mistakes Jekyll theme).
- **Generator**: Jekyll (Ruby), managed with Bundler (`Gemfile` / `Gemfile.lock`).
- **Hosting**: GitHub Pages, served from a user-site repo named `Maxjiang03.github.io`.
- **Content format**: Markdown + YAML front matter; behavior configured in `_config.yml` and `_data/`.
- **Local dev**: `bundle install`, then `bundle exec jekyll serve` -> preview at `http://localhost:4000`.

Do **not** introduce extra build tooling (npm, bundlers, JS frameworks) in v1. Stay within the
Jekyll / AcademicPages workflow.

---

## 3. Site Scope (v1)

Exactly **five** navigation entries, nothing more:

1. **Home** - `/`
2. **Publications** - `/publications/`
3. **Projects** - `/projects/`
4. **CV** - `/cv/`
5. **Contact** - `/contact/`

Anything outside this scope (talks, teaching, blog/posts, portfolio guide, talk map) must be
**removed, not merely hidden**.

---

## 4. Directory Structure

AcademicPages ships with more than we need. Target structure **after cleanup** (key items):

```
.
├── _config.yml              # site + author config; collections; plugins
├── _data/
│   └── navigation.yml       # the 5 nav items only
├── _pages/
│   ├── about.md             # HOME  (front matter: permalink: /)
│   ├── publications.md      # Publications archive  (/publications/)
│   ├── projects.md          # Projects archive      (/projects/)  <- renamed from portfolio.md
│   ├── cv.md                # CV page               (/cv/)  links to the PDF
│   └── contact.md           # Contact page          (/contact/)
├── _publications/           # one .md (the single confirmed paper)
├── _portfolio/              # one .md per project (collection stays `portfolio` internally; see note)
├── _layouts/                # template layouts (Liquid) - edit minimally
├── _includes/               # template partials       - edit minimally
├── _sass/ , assets/         # styles
├── files/
│   ├── Yixian_Jiang_CV.pdf                         # PUBLIC (redacted) CV - see 6.7
│   └── jiang2026-hierarchical-command-detection.pdf  # the published paper (public)
├── images/
│   └── profile.jpg          # sidebar avatar = the author's professional headshot
├── Gemfile / Gemfile.lock
└── CLAUDE.md                # this file
```

**Delete after fork**: `_pages/talks.md`, `_pages/teaching.md`, `_pages/year-archive.md`, the
markdown/guide page, `_talks/`, `_teaching/`, all sample `_posts/`, `talkmap/`, and any unused
`markdown_generator/`. Remove every sample item inside `_publications/` and `_portfolio/`. Trim
unused sample images.

**Note on Projects**: to minimize template breakage in v1, keep the underlying Jekyll collection
named `portfolio` (folder `_portfolio/`, collection config unchanged). Only the **page, permalink,
title, and nav label** become "Projects". A full rename of the collection to `projects` is an
optional later cleanup.

---

## 5. Editing Boundaries

- **Edit freely**: `_config.yml`, `_data/navigation.yml`, everything under `_pages/`,
  `_publications/`, `_portfolio/`, `files/`, `images/`.
- **Edit cautiously and verify the build**: `_layouts/`, `_includes/`, `_sass/`. Make the smallest
  change that achieves the goal; never wholesale-rewrite template internals in v1.
- After **any** change, the site must build cleanly (`bundle exec jekyll serve`) and have **no
  broken links** before committing.

---

## 6. Content Conventions

### 6.1 Source of truth & accuracy
The verified facts in **Appendix A** are the single source of truth. Do not add, infer, or embellish
anything not supported there. If something is uncertain, leave a clearly marked `TODO` for the
author rather than guessing. **Never package or upgrade a piece of work into something it is not**
(e.g., research experience must not be presented as a paper).

### 6.2 Publications (`_publications/`)
One file per **confirmed** publication. v1 contains exactly **one** publication (see Appendix A).
Required front matter:

```yaml
---
title: "Full Paper Title"
collection: publications
permalink: /publication/<slug>
date: 2026-05-01                       # real date, YYYY-MM-DD
venue: "Cyber Science 2026"            # real venue
status: "Accepted"                     # see taxonomy in 6.4
excerpt: "**[Accepted ...]** 1-2 sentence plain-language summary of the contribution."
paperurl: "/files/<paper>.pdf"         # ONLY a real URL/path; otherwise leave empty / omit
codeurl: ""                            # ONLY a real URL; otherwise leave empty / omit
citation: 'Yixian Jiang, Qinzheng Hu, Pavandeep Singh Baxi. ...'   # real citation
---
Optional longer body in Markdown.
```

For co-first authorship, mark the equal contributors and state it explicitly (see Appendix A).

### 6.3 Projects (`_portfolio/`, displayed as "Projects")
One file per project. Required front matter:

```yaml
---
title: "Project Title"
collection: portfolio
permalink: /portfolio/<slug>
type: "Course Project"                  # see taxonomy in 6.4
period: "Jan 2026 - Mar 2026"           # real timeframe (displayed)
stack: "Rust, ..."                      # key tools/tech
excerpt: "**[<type> · <period>]** 1-2 sentences: problem, method, concrete contribution."
codeurl: ""                             # ONLY a real URL; otherwise omit
---
Optional longer body.
```

**Ordering**: control project order with a numeric filename prefix (e.g. `01-...md`, `02-...md`).
Do **not** add a `date` field to portfolio items - it would override the filename ordering.

### 6.4 Status / type taxonomy (use exactly one; never inflate)

**Publication `status`:**
- `Accepted` - accepted/published at a named venue (include venue + year; say "to appear" until the
  proceedings are out).
- `Under Review` - submitted, decision pending.
- `In Preparation` - manuscript being written, not yet submitted.
- `Technical Report` / `Preprint` - self-archived (e.g. arXiv) with no peer-reviewed venue.

**Project `type`:**
- `Research Project` / `Research Experience` - exploratory or ongoing research that is **not** a paper.
- `Undergraduate Thesis` (or `Thesis`).
- `Collaborative Research` - cross-institution collaboration.
- `Course Project` - coursework deliverable (name the course in the body if useful).
- `Technical Report` - standalone technical write-up.
- `Competition` - competition entry.

### 6.5 Badges
Render each item's `status` / `type` as a small badge next to the title so it is immediately
scannable. **v1 implementation**: lead the `excerpt` with a bold tag, e.g. `**[Accepted ...]**` or
`**[Course Project · Jan 2026 - Mar 2026]**`. This renders without touching layouts while keeping the
structured `status` / `type` field as the source of truth. A proper badge (a small edit to
`_includes/archive-single.html` reading the field) is an optional later improvement. Never display a
status more advanced than reality.

### 6.6 Links
Only link to resources that actually exist. If there is no paper PDF, code repo, or slides, **omit
the link entirely** - do not create placeholder or fabricated URLs.

### 6.7 Privacy (hard requirement)
Public pages (author sidebar + Contact) may display only:
- **Email**, **GitHub**, **ORCID**, **LinkedIn** - allowed (links confirmed; see Appendix A).
- **Google Scholar** - none. The author does not maintain one; do not add or reference it.

**Never publish**: phone number, home address, student / matric number, transcript, grades, family
information, or **any ID card / personal-document image** (e.g. the uploaded `Youth_Card.png`).

**Email caveat**: do **not** publish `your matric-bearing student email` - it embeds the matric/student
number. Use a personal/academic address instead. Left as `TODO` for the author to set.

**CV PDF caveat**: the file at `files/Yixian_Jiang_CV.pdf` must be a **redacted public version** with
the phone number, home address, and matric/student number removed. The author's source CV currently
contains all three; do not publish it unredacted.

---

## 7. Design Conventions

- **Aesthetic**: clean, restrained, high information density, mobile-first. Inspired by Sizhe Chen's
  homepage (single content column + author sidebar, badge-annotated entries) but **not a copy** -
  do not reuse its text or bespoke styling verbatim.
- **Palette**: neutral background, dark high-contrast text, and a single restrained accent color for
  links/badges. No gradients, no bright/flashy colors.
- **Typography**: use the template's default readable stack or one clean font. Do not load heavy
  webfonts; legibility and performance come first.
- **Layout**: AcademicPages default single-content-column with the author profile sidebar. Generous
  whitespace; let the content breathe.
- **Skin / dark mode**: keep the default light skin for v1. Dark mode is a later enhancement.
- **Responsiveness**: verify layout at mobile (~375px), tablet, and desktop widths before treating a
  page as done.
- **Avatar / favicon**: use the author's professional headshot at `images/profile.jpg` for the
  sidebar avatar; set a simple favicon. Use a placeholder only if an asset is missing, marked `TODO`.

---

## 8. Development Workflow & Git Discipline

- **Content/presentation separation**: all personal facts, the publication, and projects live in
  data/content files (`_data/`, `_publications/`, `_portfolio/`, `_pages/`). Updating content must
  not require touching layout or style code.
- **Small, focused commits**: one logical change per commit, with a clear message
  (e.g. `content: add Cyber Science 2026 publication`, `config: trim nav to five items`). Do not
  bundle unrelated changes.
- **MVP first, polish later**: get a deployable skeleton building early, then iterate. Each commit
  should leave the site buildable.
- **Verify before commit**: run a local build, click through all five pages, confirm no broken links
  and correct rendering on mobile and desktop.
- **Do not push or change repo settings without the author's approval** (pushing publishes the site).
- **No secrets** in the repo (no API keys, tokens, credentials).

---

## 9. Prohibitions (hard rules)

1. **No fabrication or exaggeration** of any fact: the publication, venues, dates, citations, links,
   authorship, awards, roles, affiliations, or metrics. Accuracy is non-negotiable.
2. **No status inflation**: never label `In Preparation` / `Under Review` work as `Accepted`; never
   present research experience or a course project as a publication.
3. **The LVLM work is NOT a publication**: it must not appear under Publications and must not carry
   any publication status. It is a Research Project / Research Experience only.
4. **No invented URLs**: omit a link rather than fabricate a paper/code/slides link.
5. **No private data** on public pages: no phone, home address, matric/student number, transcript,
   grades, family info, or any ID card image (e.g. `Youth_Card.png`) (Section 6.7).
6. **No scope creep in v1**: do not (re)add talks, teaching, blog/posts, or pages beyond the five.
7. **No heavy tooling / framework**: stay within Jekyll + AcademicPages; no npm/JS frameworks for v1.
8. **No broken builds or links** in committed states.
9. **No verbatim copying** of the reference site's text or bespoke design.
10. **No large, unrelated refactors** in a single commit.

---

## 10. Follow-up Task List (ordered)

Work top to bottom; each item is a small, separately committable step.

**Setup**
1. Ensure the local Jekyll environment builds (`bundle install`; `bundle exec jekyll serve`). Confirm
   the repo is the user site `Maxjiang03.github.io`.

**Configuration & cleanup**
2. Edit `_config.yml`: site `title`, `description`, `url: https://Maxjiang03.github.io`,
   `repository: Maxjiang03/Maxjiang03.github.io`, author block; remove analytics and unused settings;
   reduce collections to `publications` and `portfolio` (remove `talks`, `teaching`).
3. Set `_data/navigation.yml` to exactly the five items (Home, Publications, Projects, CV, Contact).
4. Delete all default sample content and unused pages/collections/images (see Section 4).

**Core pages**
5. Author sidebar: avatar (`images/profile.jpg`), one-line bio, location, links
   (Email [TODO], GitHub, ORCID, LinkedIn).
6. Home (`_pages/about.md`): a restrained 3-4 sentence bio + a short "Research Interests" list
   covering the four lines + pointers to Publications/Projects/CV.
7. Publications: create `_pages/publications.md`; add the **one** confirmed publication
   (Cyber Science 2026, *Accepted - to appear*) with full author list and the equal-contribution
   note. Appendix A.
8. Projects: rename the portfolio page to `_pages/projects.md` (title "Projects",
   permalink `/projects/`); add the six confirmed projects with correct `type`, **including the LVLM
   work as a Research Project (not a publication)**. Appendix A.
9. CV: link to the redacted public `files/Yixian_Jiang_CV.pdf` from `_pages/cv.md`.
10. Contact: `_pages/contact.md` with Email [TODO], GitHub, ORCID, LinkedIn (no phone/address/ID).

**Polish & ship**
11. Design pass: neutral palette + single accent, readable type, consistent badges; fix
    Minimal-Mistakes leftovers (footer "© Your Name", sample copy); set favicon.
12. SEO/meta: accurate `title`/`description`, Open Graph image, sitemap; ensure name + research
    keywords appear for discoverability.
13. QA: clean build, no broken links, proofread for factual accuracy, verify mobile + desktop.
14. Prepare for deploy; the author reviews and pushes to publish at `https://Maxjiang03.github.io`.

**Later (not v1)**
15. Optional: dark mode, proper status badges, custom domain.

---

## Appendix A - Verified Content (Source of Truth)

> Drawn from the author's CV, the published paper, and the author's latest confirmations.
> Authoritative for v1. Mark anything unverifiable as `TODO` rather than guessing.

**Identity**
- Name (display): **Yixian Jiang**
- Current: MSc Cybersecurity, **University of Glasgow**, School of Computing Science
  (Sept 2025 - Sept 2026, expected).
- Research Assistant, **State Key Laboratory of Complex and Critical Software Environments
  (SKLCCSE), Beihang University** (Oct 2025 - present). Advisors: Prof. Xianglong Liu and
  Prof. Aishan Liu. Topic: LLM adversarial jailbreaking.
- Previously: BEng in Information Security, **North China University of Technology (NCUT)**, School
  of AI and Computer Science (Sept 2021 - June 2025; GPA 84/100). Research Assistant, IoT & Privacy
  Security Lab, NCUT (Nov 2024 - June 2025); advisor: Prof. Gang Xu.

**Research interests (the four lines)**: Secure and Trustworthy Agentic AI Systems; LLM Security;
AI-enabled Cyber Defence; IoT/ICS Security.

**Publications (v1: exactly ONE confirmed paper)**
1. *Hierarchical Detection of Malicious Command Lines Using Random Forest and Context-Aware LSTM*
   - Authors: **Yixian Jiang**, Qinzheng Hu, Pavandeep Singh Baxi - School of Computing Science,
     University of Glasgow.
   - **Equal contribution: Yixian Jiang and Qinzheng Hu contributed equally to the manuscript.**
     Mark both as co-first authors; bold "Yixian Jiang" in the rendered entry.
   - ORCIDs: Yixian Jiang 0009-0005-9180-9757; Qinzheng Hu 0009-0009-1544-0432;
     Pavandeep Singh Baxi 0009-0008-0047-1925.
   - Venue: **Cyber Science 2026** (conference paper). **Status: Accepted** (to appear).
   - Summary (from the abstract; do not exaggerate): a hierarchical framework that combines
     feature-based machine learning with sequence-aware LSTM modeling within a unified evaluation.
     Random Forest is strongest for single-command detection, while RF+LSTM gives the best
     command-stream (multi-step) detection. Built as a Rust-based prototype with lightweight
     deobfuscation and a 172-dimensional feature representation.
   - Links: paper PDF at `/files/jiang2026-hierarchical-command-detection.pdf` (author will place it).
     Code: none public yet - leave a `TODO`, do not invent a URL.

> The **LVLM adversarial robustness work is NOT a publication**. It is no longer being written and
> will not be submitted or published. It must never appear under Publications or carry any
> publication status (`In Preparation` / `Under Review` / `Accepted`). It belongs under Projects as a
> Research Project (see below).

**Projects**
1. *Adversarial Robustness Study of Large Vision-Language Models* - **Type: Research Project**
   (Oct 2025 - present). Exploratory study on the adversarial robustness of large vision-language
   models under mixed visual-text attack settings, focusing on attack formulation, evaluation design,
   and robustness analysis. Conducted as research experience at SKLCCSE, Beihang University.
   **Not a paper / not a publication.**
2. *Industrial Control System Security Platform based on CNN-LSTM* - **Type: Undergraduate Thesis**
   (Nov 2024 - June 2025). CNN-LSTM model for real-time anomaly-based intrusion detection in ICS;
   Digital Twins to simulate chemical plants; integrated alerting and cyber-risk mitigation.
3. *Programmable SDN Controller for Multi-Path Load Balancing* - **Type: Course Project** (Systems &
   Networks), Jan 2026 - Mar 2026. Ryu/OpenFlow 1.3 controller for multi-path routing and load
   balancing in Mininet; evaluated connectivity and throughput with Open vSwitch and iperf3.
4. *Emoji++ Interpreter in Rust* - **Type: Course Project** (Secure Systems Programming),
   Feb 2026 - Mar 2026. Rust CLI interpreter with file input, configurable memory, debug modes, loop
   control, and runtime error handling; Rust type system + boundary checks for memory safety.
5. *Privacy Protection Scheme based on Blockchain and CP-ABE* - **Type: Collaborative Research**
   (with Beijing University of Posts and Telecommunications), Nov 2024 - Feb 2025. CP-ABE in Go for
   fine-grained access control in multi-cloud; reduced user-side overhead by outsourcing storage and
   computation.
6. *Consortium Blockchain-based Vehicle Trajectory Monitoring* - **Type: Competition** (National
   Cryptographic Technology Competition), Sept 2023 - Nov 2023. PBFT consensus for resource-constrained
   vehicle nodes; trajectory data secured on-chain via identity verification.

**Skills**: Python, Rust, C/C++, Java, Go, Assembly, SQL, Unix; PyTorch, Hugging Face Transformers,
TensorFlow, Scikit-learn.

**Selected awards** (use only where a section calls for it; keep accurate): Third Prize, China
International College Students' Innovation Competition Finals 2025 (Aug 2025); Third Prize, NCUT
Mathematics Competition (June 2022); Second Prize, National Final, National Foreign Language
Proficiency Competition (May 2022); Innovation Scholarship, NCUT (Sept 2022).

**Service**: Class Representative, Cybersecurity MSc (Sept 2025 - Sept 2026, expected).

**Contact / public links**
- Email: `TODO` - a personal/academic address; **not** the matric-bearing student email.
- GitHub: https://github.com/Maxjiang03
- ORCID: https://orcid.org/0009-0005-9180-9757
- LinkedIn: https://www.linkedin.com/in/yixian-jiang-50906733a/   (confirmed)
- Google Scholar: none (not maintained) - do not add or reference.
- Location: Glasgow, UK.
- **Do not publish**: phone number, home address, matric/student number, transcript, grades, family
  info, or any ID card image (e.g. `Youth_Card.png`).

**Assets provided by the author**
- `images/profile.jpg` - professional headshot (sidebar avatar).
- `files/Yixian_Jiang_CV.pdf` - REDACTED public CV (phone/address/matric removed).
- `files/jiang2026-hierarchical-command-detection.pdf` - the published paper (public).
- `Youth_Card.png` (in uploads) - **must never be used or published**; it is an ID card with personal
  data.
