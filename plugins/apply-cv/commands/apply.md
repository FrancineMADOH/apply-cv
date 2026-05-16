---
description: "Analyse a job offer and prepare a complete application dossier — reads your CVs from the current folder"
argument-hint: <path-to-offer-file>
allowed-tools: [Read, Write, Edit, Glob, Grep, Bash]
---

Analyse a job offer and prepare a complete application dossier based on the CVs found in the current directory.

**Offer file:** $ARGUMENTS

When this command is invoked, scan the current directory for CVs, read the offer file, then execute the following steps in order. Stop only if the result is a hard NO-GO.

---

## STEP 0 — CANDIDATE PROFILE DISCOVERY

Before anything else, scan the current directory for available CVs.

**Search:** find all files with extensions `.md`, `.pdf`, `.docx`, `.doc`, `.txt` whose name contains "CV", "cv", "resume", "Resume", or "curriculum". Also check subdirectories named `cv`, `CVs`, `resumes`, or `cv_variants`.

**If no CV is found:** stop and display this message:
> No CV found in the current directory. Please add your CV file(s) here (supported formats: .md, .pdf, .docx, .txt) and run `/apply` again.

**If one or more CVs are found:**
1. Read all found CVs
2. Extract and consolidate the candidate profile:
   - Full name
   - Contact info (email, phone, LinkedIn if present)
   - Professional experiences (company, role, dates, key responsibilities)
   - Key skills (functional, technical, tools)
   - Education
   - Languages and proficiency levels
   - Availability if mentioned
   - Salary expectations if mentioned
   - Mobility / preferred locations if mentioned
3. Keep this profile in memory — it replaces any hardcoded reference for all subsequent steps

**If multiple CVs are found:** note the variants available (different titles, different focus areas). You will use them in Step 3.2 to select the best match for the offer. Do not ask the user to choose — you decide.

---

## STEP 1 — READ THE OFFER

Read the file provided as argument (`$ARGUMENTS`). Extract and summarize:
- Company + sector
- Exact job title
- Location + remote possible
- Required experience
- Main responsibilities (list)
- Required skills (mandatory vs. preferred)
- Required certifications
- Salary if mentioned
- Contract type (permanent, fixed-term, freelance...)
- Cover letter explicitly required? (yes/no)

**Detect the language of the offer (French or English) — all generated documents will be in that language.**

---

## STEP 2 — GO / NO-GO DECISION

Apply the following grid objectively, based on the candidate profile extracted in Step 0:

### IMMEDIATE NO-GO (stop, explain why)
- 100% technical role with no functional or management dimension (pure DevOps, SysAdmin, Data Engineer, pure developer with no BA/PM component)
- Required experience **7 years or more**, explicitly and strictly stated
- **Mandatory** certification the candidate does not have according to their CVs
- Domain with no transferable skills whatsoever (actuarial science, civil/mechanical engineering, law, pure market finance, clinical medicine)

### GO (recommend applying)
- At least 3 out of 5 responsibilities match the candidate's profile directly
- Required experience ≤ 6 years
- The role has a functional, analytical, project management, or AI dimension
- Location within the candidate's stated mobility zone (or remote)

### GREY ZONE — GO WITH RESERVATIONS (flag clearly)
- 5–6 years required and candidate has less (gap to compensate with skills — mention explicitly)
- Certification "preferred" but not mandatory
- Sector without direct experience but with clear transferable skills
- Hybrid tech/functional role with significant dev component

**Display clearly:** `✅ GO`, `⚠️ GO WITH RESERVATIONS` or `❌ NO-GO` with a 2–3 line justification.

---

## STEP 3 — IF GO OR GO WITH RESERVATIONS: CREATE THE DOSSIER

### 3.1 Folder
Format: `YYYY-MM-DD_CompanyName_Role/` (spaces replaced by `_`, all lowercase)
Path: `./candidatures/` (relative to the current directory — create if it does not exist)

Create the folder and copy the offer inside as `offre.txt`.

### 3.2 Select and adapt the best CV

**Selection rule:**
1. Identify which CV variant (from Step 0) is closest to the role
2. Calculate an alignment score (% of required skills covered)
3. **If score ≥ 75%:** adapt the selected CV — reorder skills to highlight what matches, adjust the title if needed, integrate 2–3 keywords from the offer
4. **If score < 75% or atypical hybrid role:** create a tailored CV by merging the most relevant elements from multiple CVs

Name the file: `CV_[CandidateFullName]_[CompanyName].md`

**Never invent skills or experiences.** Adapting = reordering, rephrasing, emphasising what is already there.

### 3.3 Create the offer analysis

Create `analyse_offre.md`:

```
# Analysis — [Role] at [Company]
Date: YYYY-MM-DD

## Offer Summary
[3–4 lines]

## Decision: GO / GO WITH RESERVATIONS / NO-GO
[Justification]

## Profile / Offer Alignment
| What the offer requires | What the candidate brings | Match level |
|---|---|---|
| [skill 1] | [concrete experience] | ✅ Strong / ⚠️ Partial / ❌ Missing |

## Key strengths to highlight for this role
- [point 1]
- [point 2]
- [point 3]

## Weaknesses / gaps to address
- [if applicable]

## CV selected
[CV name + reason]

## Customisations made to the CV
- [list of adjustments]
```

### 3.4 Create the application email

Create `email_candidature.md`:
- Language matches the offer language
- Subject line: `Application — [Exact job title] — [Candidate full name]`
- Maximum 3 paragraphs: hook (why this company), value proposition (2–3 profile highlights relevant to the offer), closing (availability, attachments)
- Professional, direct tone — no hollow phrases
- Full signature with contact details extracted from the CV

### 3.5 Create the cover letter (ONLY if explicitly required in the offer)

If required: create `lettre_motivation.md`
- Maximum 1 page (3–4 paragraphs)
- Structure: hook → why this role/company → what I bring (concrete examples) → conclusion
- Based on offer elements and the most relevant experiences from the candidate profile

---

## STEP 4 — UPDATE TRACKING

Look for `./candidatures/tracking.md`.

**If it does not exist**, create it with the following header:

```markdown
# Application Tracking

| Date | Company | Role | Source | Status | Folder | Notes |
|---|---|---|---|---|---|---|
```

Then add a row:

```
| YYYY-MM-DD | [Company] | [Role] | [Source if visible in the offer] | A_ENVOYER | [folder_name] | [short notes: match score, any reservations] |
```

---

## STEP 5 — FINAL SUMMARY

Display:
```
📋 OFFER   : [Role] at [Company]
✅/⚠️/❌ DECISION : [GO / GO WITH RESERVATIONS / NO-GO]
📁 DOSSIER : candidatures/[folder_name]/
📄 CV      : [CV file used] — [estimated alignment %]
📧 Email   : ready
📝 Cover   : [yes / no]
⚠️  Watch  : [if grey zone — key points to address]
```

If NO-GO: display only the decision and justification. Do not create any folder or file.
