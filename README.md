# IBU PODx Newsletter

Monthly newsletter for the **IBU Personalisation, Omnichannel & Digital** team at Eli Lilly.

🔗 **Live edition:** https://agentvebz.github.io/ibu-podx-newsletter/
📚 **Archive:** https://agentvebz.github.io/ibu-podx-newsletter/archive.html
📅 **Cadence:** Monthly · First edition June 1, 2026

---

## 📁 Repository Structure

```
ibu-podx-newsletter/
├── index.html              ← Latest edition (always current month)
├── archive.html            ← Archive landing page with all editions
├── editions/               ← Permanent per-month URLs
│   ├── 2026-04-april.html
│   ├── 2026-05-may.html
│   └── ...
└── README.md               ← This file
```

---

## 🤝 Team Collaboration Norms

We work on a **personal repo with collaborators** rather than a full organization, which means GitHub can't enforce rules — *we* enforce them. These norms keep the repo healthy without being bureaucratic. Read once, then internalize.

### 🌳 Branching Strategy

**`main` is sacred** — only merged, reviewed editions live here. The current state of `main` is what readers see on SharePoint **right now**.

**Always create a branch for any work**, named with this convention:

| Type of work | Branch name pattern | Example |
|---|---|---|
| New monthly edition | `editions/YYYY-MM-monthname` | `editions/2026-05-may` |
| Skill / template change | `skill/<short-description>` | `skill/add-event-section` |
| Quick content fix | `fix/<short-description>` | `fix/typo-canada-section` |
| Design / styling tweak | `design/<short-description>` | `design/improve-mobile-spacing` |

```bash
# Always do this before starting any work
git checkout main
git pull origin main
git checkout -b editions/2026-05-may

# ... make your changes ...

git add .
git commit -m "Add May 2026 edition (Issue #02)"
git push -u origin editions/2026-05-may
```

### 🚦 What Goes Through PR Review (and What Doesn't)

| Change Type | PR Required? | Min Reviewers |
|---|---|---|
| **Monthly edition publish** | ✅ Yes | 1  |
| **New section added to design** | ✅ Yes | 1  |
| **Skill / scripts modified** | ✅ Yes | 1 |
| **Typo / link fix** | ❌ No — direct push to `main` OK | — |
| **Adding a card to archive** | ❌ No — direct push OK | — |
| **README updates** | ❌ No — direct push OK | — |

### ✍️ Commit Message Format

Keep messages descriptive and skim-friendly:

✅ Good:
```
Add May 2026 edition (Issue #02) + archive April
Fix mobile breakpoint for KPI grid on small screens
Update Forms schema to include "milestone" type
```

❌ Avoid:
```
Update
fix stuff
asdfasdf
final final v2
```

**Rule of thumb:** if someone reads only the first line of your commit message, they should know what changed.

### 🔄 Pull Request Etiquette

When opening a PR:
1. **Title:** Same format as commit message (descriptive, one line)
2. **Description:** Brief context — what changed, why, anything reviewer should focus on
3. **Tag a reviewer:** Use `@username` — tag the rotating proof-reader for editions, the editor-in-chief for skill/design changes
4. **Self-review first:** Click the "Files changed" tab on your own PR before tagging anyone — catch obvious issues yourself
5. **Don't merge your own PR** for monthly editions — get one approval first
6. **Delete the branch after merge** — keeps the repo clean

### 🚨 Direct-to-`main` Push (Allowed but Use Sparingly)

For trivial fixes (typos, broken links, single-line README updates):

```bash
git checkout main
git pull origin main
# make tiny fix
git add .
git commit -m "Fix broken Teams link in resources"
git push origin main
```

⚠️ **Do not push to main if:**
- The change is content-related (use a branch)
- You're not 100% sure it's correct
- It touches `index.html` body content
- It modifies any script in `scripts/`

When in doubt → **use a branch.**

### 🆘 Conflict Resolution

If `git pull` shows merge conflicts:

```bash
# Step 1: don't panic, don't force push
git status  # see what's conflicted

# Step 2: open the conflicted files, fix the markers manually
# look for <<<<<<< HEAD and >>>>>>>

# Step 3: after fixing all conflicts
git add .
git commit -m "Resolve merge conflict with main"
git push origin <your-branch>
```

If you're not sure how to resolve a conflict, **ask the editor-in-chief in the team chat before force-pushing anything**. Force pushes can erase work permanently.

### 🔐 Authentication Setup

First time cloning? Don't use a password — GitHub disabled that. Two options:

**Option A: GitHub CLI (Recommended)**
```bash
# Install once
brew install gh                # Mac
winget install --id GitHub.cli # Windows
# or download from cli.github.com

# Authenticate
gh auth login
# Choose: GitHub.com → HTTPS → Login with web browser
```

**Option B: Personal Access Token**
1. github.com → top-right avatar → Settings
2. Developer settings → Personal access tokens → Tokens (classic)
3. Generate new token → scope: `repo`
4. Copy token → use as password when git prompts

⚠️ **Treat tokens like passwords.** Don't paste them in chat or commit them to the repo.

### 🛡️ Repository Hygiene

**Don't commit:**
- ❌ Secrets, API keys, tokens, passwords
- ❌ Personal data of any kind
- ❌ Internal Lilly documents (PowerPoints, spreadsheets) unrelated to PODx
- ❌ Patient/HCP data (always — even in test files)
- ❌ Submission Excel files (these belong on SharePoint, not GitHub)

**Do commit:**
- ✅ HTML / CSS / JS for the newsletter
- ✅ The skill (when migrated to repo)
- ✅ Documentation (this README, references)
- ✅ Sample/anonymized test data clearly marked as such

### 📅 Working in Parallel

If two people need to work on different things simultaneously:
- ✅ Each creates their own branch from latest `main`
- ✅ Each commits to their own branch
- ✅ First merger wins; second merger pulls and resolves any conflicts
- ⚠️ **Don't both edit `index.html`** at the same time — coordinate in chat first

---

## 🔄 Monthly Workflow (Tier 2 Semi-Auto)

### Week 2 of each month — Submission Window Opens

1. Power Automate sends MS Forms link to all IBU via Teams + Email
2. Team submits content (achievements, automation tips, hobbies, jokes, etc.)
3. Submissions auto-aggregate into SharePoint List `PODx-Submissions-YYYY-MM`

### 25th of each month — Editor's Working Session (~30 mins)

1. Open Power Automate flow → exports SharePoint List → emails Excel to editor
2. Open Claude with **PODx Skill** loaded
3. Upload `PODx-Submissions-YYYY-MM.xlsx`
4. Prompt: *"Build the [Month] [Year] PODx edition"*
5. Claude generates `index.html` following the skill's content rules
6. Editor reviews, makes manual tweaks if needed

### 28th of each month — Publish

1. Create branch:
   ```bash
   git checkout -b editions/2026-05-may
   ```
2. Save outgoing edition:
   ```bash
   cp index.html editions/2026-04-april.html
   ```
3. Replace `index.html` with the new edition Claude generated
4. Update `archive.html` — add new card for the just-archived edition (Claude provides the block)
5. Commit + push:
   ```bash
   git add .
   git commit -m "Add May 2026 edition (Issue #02) + archive April"
   git push -u origin editions/2026-05-may
   ```
6. Open Pull Request, tag rotating reviewer, wait for approval
7. Merge to `main`
8. GitHub Pages auto-deploys in ~30 seconds
9. SharePoint embed automatically picks up new content

---

## 🛠️ The Tech Stack

- **Hosting:** GitHub Pages (free, static, public)
- **Design:** Hand-rolled HTML + CSS + vanilla JS (no frameworks)
- **Fonts:** Google Fonts — DM Serif Display + DM Sans + JetBrains Mono
- **Animations:** Pure CSS + Canvas API + SVG
- **Embed:** SharePoint Modern Page · Embed web part · iframe
- **Content generation:** Claude (with custom PODx Skill)
- **Submissions:** Microsoft Forms → Power Automate → SharePoint List
- **Archive:** Per-month files in `/editions/` + searchable `archive.html`

---

## 🎨 Design System

| Element | Value |
|---|---|
| Primary | `#D52B1E` (Lilly Red) |
| Surface dark | `#1A2B4A` (Navy) |
| Accent dark | `#4A1F5C` (Plum) |
| Surface light | `#F7F8FA` (Mist) |
| Headings font | DM Serif Display |
| Body font | DM Sans |
| Mono font | JetBrains Mono |
| Wrapper width | 100% (edge-to-edge for iframe) |

---

## 📝 Content Rules

### Never include
- HCP personal information or names
- Patient data (PHI)
- Commercially sensitive sales / pricing data
- External brand IP without licensing


### Always include
- "Internal Use Only" footer disclaimer
- Editor signature in Editor's Note
- Mobile responsive breakpoints (720px and 420px)
- Live timezone clocks (Indianapolis + Bengaluru)

---

## 📨 Submission Form Schema

| Form Field | Maps to |
|---|---|
| Name + Team | Editor sig + Our People |
| Achievement | Achievements |
| Spotlight nominee | Person of the Month |
| Automation tip | Automation Spotlight |
| Training/cert | Knowledge & Learning |
| Personal win / hobby | Our People |
| Joke or meme | Fun Corner |
| Team reminder | Reminders |

---

## 📊 SharePoint Embed Code

```html
<iframe src="https://agentvebz.github.io/ibu-podx-newsletter/"
        width="100%" height="8500"
        frameborder="0" scrolling="auto"
        style="border:none;"></iframe>
```

Adjust `height` per edition — typically 7500–8500px depending on section count.

---

## 🆘 Common Issues

**Newsletter not updating in SharePoint** — GitHub Pages caches for ~10 mins. Hard-refresh the SharePoint page (Ctrl+Shift+R) or wait.

**Iframe shows scrollbar inside** — Increase `height` attribute. Find the right number once, then keep it constant per edition.

**Animations stutter on mobile** — The constellation canvas particles and morphing blobs are GPU-intensive. They auto-throttle on low-power devices via `requestAnimationFrame`.

**Forms questions changed** — Update the PODx Skill's submission form schema mapping table accordingly.

**"Permission denied" when pushing** — You're not authenticated. See the **Authentication Setup** section under Team Collaboration Norms above.

**"Updates were rejected" when pushing** — Someone pushed to `main` while you were working. Run `git pull origin main` (or your branch), resolve any conflicts, push again.

**Accidentally committed something sensitive** — Don't push it. Run `git reset --soft HEAD~1` to undo the commit while keeping changes. Then fix and recommit. If you've already pushed, **immediately tell the editor-in-chief** — they'll need to force-push a clean version.


---

© 2026 Eli Lilly and Company. Internal use only.
