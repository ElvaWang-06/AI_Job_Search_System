# Resume Format

This is the layout contract. Content selection is resume-tailor's job; this skill only governs how the document looks, what it's called, and whether it survives an ATS parse.

Never improvise formatting. Every value below is fixed.

## File name (required — no exceptions)
[LastName]_[Role]_[Company]_[MonthYear].docx
Company	Company name, no spaces, CamelCase if multi-word	Mercor, HarvardArtMuseums
MonthYear	3-letter month + 2-digit year, no separator	Jul26

The same string (minus .docx) is what goes in the tracker's Resume Version column, so it must match exactly. Pass it as the argument to build_resume.js; the script rejects anything that doesn't match the pattern.

Track selection: pick the one matching the JD's primary function, not Elva's degree. An assessment/measurement/analytics role is Eval; a pure data-science role is Data.

## Page setup
Property	Value	DXA (twips)
Page size	A4	11906 × 16838
Margin — top	0.35"	504
Margin — bottom	0.35"	504
Margin — left	0.25"	360
Margin — right	0.5"	720
Usable text width	7.52"	10826

⚠️ Set page size explicitly in docx-js — never rely on the default.

## Typography
Font: Times New Roman. One font for the entire document, including headers.
Size: 10pt (size: 20 half-points) for EVERY run — including the name. The name is bold, not enlarged.
Never change the type to make content fit. No 9pt, no condensed line spacing, no shaved margins. Fit by cutting content (see §6).
Color: black. Hyperlinks: default Word hyperlink style.
Inline bold inside bullets highlights metrics and lead actions (**needs assessment with 20+ stakeholders**, **65%**). Keep this — it's the signature of the template — but bold no more than ~1/3 of any bullet.
3. Section order
Name + contact line
Education
Technical Skills
Work Experience
Project Experience

No Summary / Objective paragraph unless explicitly requested. Skills sit high (right after Education), not at the bottom.

Section names may be adapted to the target role (e.g. "Work Experience" → "Evaluation & Measurement Experience") but keep them ATS-standard (§5) and keep the order — education, skills, work, projects.

## Paragraph specs
Element	Spec
Name	Centered · bold · 10pt
Contact	Centered · 10pt · indent left 360 · |-separated: email | phone | LinkedIn | Website
Section header	Bold · 10pt · indent left 360 · bottom border (single, size 1, black) · right tab at 10826 · Title Case, not ALL CAPS
Org line	Indent left 360 · right tab at 10466 · spacing before: 120 (6pt) · **Company**, City, ST → TAB → Mon YYYY – Mon YYYY (en-dash; current roles end in Current)
First org line under a section header	Same as Org line but spacing before: 0 — no blank gap between the header rule and the first entry. Only the first entry in each section; every later entry in that section keeps spacing before: 120.
Role line	Italic · 10pt · indent left 360 · directly under the org line, no spacing before
Bullet	• via numbering · indent left: 720, hanging: 360 · 10pt · single spacing · 3–4 per entry (5 max)
Skill line	Same bullet indents · **Category:** item, item, item · 3–5 category lines total

⚠️ No blank line after a section header. The header's bottom border already separates the section; an extra 6pt gap on the first entry makes the header float. In build_resume.js this is the first flag on org():

js
org("**Harvard University**, Cambridge, MA", "Aug 2025 – May 2026", true)  // first in section → before: 0
org("**Tufts University**, Medford, MA",     "Sept 2020 – May 2025")       // later entry     → before: 120

The same applies to the first Skill line under Technical Skills — it is a bullet, which has no spacing before, so it is already flush. Do not add one.

## ATS rules (hard constraints)

The layout above is already ATS-safe. Do not break it:

Single column. No tables, text boxes, columns, sidebars, graphics, icons, or skill bars — parsers drop or scramble them.
Contact info in the document body, never in a Word header/footer — many parsers never read the header.
Standard section names. Education, Technical Skills, Work Experience, Project Experience — never "My Journey", "What I Bring", "Academic Pursuits".
One font, one size throughout. Mixed sizes are a common ATS flag.
Standard bullet char (•). No →, ▪, emoji, or wingdings.
Exact JD terminology. If the JD says "Python, SQL, item response theory", use those exact strings — not "programming" or "psychometric modeling". No keyword stuffing (the same term in six variants).
Dates as Mon YYYY – Mon YYYY, consistently.

## One page — how to fit

The resume must be exactly one page.

Never: shrink the font, tighten line spacing below single, or shave the margins.

Cut in this order:

Drop the least JD-relevant entry entirely (a whole org block, not a stray bullet)
Cut entries to 3 bullets, then 2 for older/less relevant roles
Merge two related bullets into one
Collapse a Technical Skills category into another
Shorten bullet prose — trailing "by doing X" clauses go first

## Build & verify

Use scripts/build_resume.js (docx-js). It encodes every value above as helpers — section(), org(), role(), bullet(), skill() — so a new resume is just a content list. docx is preinstalled; do not run npm install.

Pre-flight checklist — run every time before delivering:

bash
NAME=Wang_Eval_Mercor_Jul26          # see §0 — must match Wang_[Track]_[Company]_[MonthYear]
node scripts/build_resume.js $NAME.docx
soffice --headless --convert-to pdf $NAME.docx
pdfinfo $NAME.pdf | grep Pages       # must read: Pages: 1
pdftoppm -jpeg -r 100 $NAME.pdf page

Then look at page-1.jpg and confirm:

 File name matches Wang_[Track]_[Company]_[MonthYear].docx (§0)
 Exactly 1 page
 Dates right-aligned, flush to the right margin (tab stops correct)
 No orphaned role line or single bullet stranded at the bottom
 No blank gap between a section header rule and its first entry (§4)
 No bullet wrapping to a single dangling word
 Times New Roman 10pt throughout — no stray size
 Section rules (bottom borders) span the full width
 Hyperlinks resolve (email, LinkedIn, portfolio)

If it renders as 2 pages, go back to §6. Do not ship a 2-page file, and do not "fix" it by changing type.

## Content rule (inherited, non-negotiable)

Master_Resume.docx is the only source of truth. Select, reorder, rewrite, and optimize — but never introduce an experience, responsibility, achievement, or metric that is not explicitly in the master. Wording upgrades that change the strength of a claim ("supported" → "led", "assisted" → "owned") go into the DELTA section for confirmation, not silently into the document.
