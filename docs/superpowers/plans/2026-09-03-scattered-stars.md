# Scattered Stars Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Sprinkle subtle unicode stars across README.md without changing layout or adding dependencies.

**Architecture:** Single-file static markdown edit in README.md — header suffix, divider accents, and trailing sparkles. No JS, no new images, no workflows.

**Tech Stack:** GitHub Flavored Markdown, unicode glyphs `✦ ˖ ˚ ⋆ ·` only.

## Global Constraints

- Style is subtle unicode only — `✦ ˖ ˚ ⋆ ·`, no emoji.
- No layout changes — keep all sections, tables, badges in place.
- No new dependencies — no JS, no external images, no Actions.
- Keep Top Langs removed — do not re-add Top Langs widget.

---

### Task 1: Header + intro scatter

**Files:**
- Modify: `README.md:1-11`
- Test: verify via grep for star glyphs

**Interfaces:**
- Consumes: current header line `## Hi, I'm Amir Asyraf ✦ Senior Full-Stack Engineer`
- Produces: header with scattered suffix `˖ ˚ ✦` and intro line trailing `⋆` for later tasks to build on

- [ ] **Step 1: Verify current header has no scatter suffix yet**

Run:
```powershell
Select-String -LiteralPath "README.md" -Pattern "˖ ˚ ✦" -SimpleMatch
```
Expected: no match (exit non-zero / empty output). This is the failing test.

- [ ] **Step 2: Run to confirm it fails**

Run: `Select-String -LiteralPath "README.md" -Pattern "˖ ˚ ✦" -SimpleMatch; if ($?) { Write-Output "FOUND" } else { Write-Output "NOT-FOUND" }`
Expected: `NOT-FOUND`

- [ ] **Step 3: Add minimal scatter to header and location line**

Edit `README.md`:
Old:
```
## Hi, I'm Amir Asyraf ✦ Senior Full-Stack Engineer
```
New:
```
## Hi, I'm Amir Asyraf ✦ Senior Full-Stack Engineer ˖ ˚ ✦
```
And old:
```
Based in Malaysia · Available for work · [amirdevs.my](https://www.amirdevs.my)
```
New:
```
Based in Malaysia · Available for work · [amirdevs.my](https://www.amirdevs.my) ⋆
```

- [ ] **Step 4: Run verification to confirm it passes**

Run: `Select-String -LiteralPath "README.md" -Pattern "˖ ˚ ✦" -SimpleMatch`
Expected: PASS with 1 match on line 1.

- [ ] **Step 5: Commit**

```bash
git add README.md
git commit -m "feat: add header star scatter"
```

### Task 2: Section divider + What I Do accents

**Files:**
- Modify: `README.md:36-44`
- Test: verify via grep for divider and trailing sparkles

**Interfaces:**
- Consumes: header scatter from Task 1 (line 1 contains `˖ ˚ ✦`)
- Produces: completed scatter — dividers use `· ✦ ·` accents, What I Do lines carry trailing sparkles

- [ ] **Step 1: Verify divider accents missing**

Run:
```powershell
Select-String -LiteralPath "README.md" -Pattern "· ✦ ·" -SimpleMatch
```
Expected: no match. This is the failing test.

- [ ] **Step 2: Run to confirm it fails**

Run: `Select-String -LiteralPath "README.md" -Pattern "· ✦ ·" -SimpleMatch; if ($?) { Write-Output "FOUND" } else { Write-Output "NOT-FOUND" }`
Expected: `NOT-FOUND`

- [ ] **Step 3: Add divider accent and trailing sparkles**

Edit `README.md` — replace first section divider after location line:
Old:
```
Based in Malaysia · Available for work · [amirdevs.my](https://www.amirdevs.my) ⋆

---

### Tech Stack
```
New:
```
Based in Malaysia · Available for work · [amirdevs.my](https://www.amirdevs.my) ⋆

· ✦ · ─ ─ ─ · ✦ ·

### Tech Stack ˖
```

Edit `README.md` What I Do trailing accents:
Old:
```
- ⌨️ **Off-hours:** Custom mechanical keyboards & writing about clean code
```
New:
```
- ⌨️ **Off-hours:** Custom mechanical keyboards & writing about clean code ˚
```
Old:
```
### Pinned Highlights
```
New:
```
### Pinned Highlights ˖
```

- [ ] **Step 4: Run verification to confirm it passes**

Run:
```powershell
Select-String -LiteralPath "README.md" -Pattern "· ✦ ·" -SimpleMatch
Select-String -LiteralPath "README.md" -Pattern "Tech Stack ˖" -SimpleMatch
Select-String -LiteralPath "README.md" -Pattern "Pinned Highlights ˖" -SimpleMatch
```
Expected: all three return matches (PASS).

- [ ] **Step 5: Final markdown sanity check**

Run:
```powershell
Get-Content -LiteralPath "README.md" -TotalCount 5
git diff --stat
```
Expected: diff touches only `README.md`, 4-6 lines changed, no Top Langs re-added. Verify with: `Select-String -LiteralPath "README.md" -Pattern "top-langs" -SimpleMatch; if ($?) { Write-Output "FAIL-TOP-LANGS-PRESENT" } else { Write-Output "OK-NO-TOP-LANGS" }` → `OK-NO-TOP-LANGS`.

- [ ] **Step 6: Commit**

```bash
git add README.md
git commit -m "feat: scatter subtle stars in dividers and sections"
```
