---
name: interview-prep
description: Research a company, role and interviewer, then produce a ≤3-page interview prep brief as a Claude Doc (company, competitors by market, AI strategy, recent moves, interviewer, pitch and fit, salary, questions). Use when the user asks to prep for an interview, recruiter screen, or hiring-manager call, or runs /interview-prep.
---

# Interview prep

Produce an actionable interview brief for the user as a **Claude Doc, max 3 A4 pages**.

## Step 0: Load the user's profile (first run sets it up)

Read `profile.md` in this skill's folder, i.e. `~/.claude/skills/interview-prep/profile.md`.

If the file doesn't exist, this is a first run. Send ONE message asking for the fields in `profile.example.md`:
- name
- current title
- location
- CV folder
- generic CV file name
- tailored CV naming pattern
- most recent salary and currency
- answer bank (optional)

Then write `profile.md` from the answers and continue. The profile is private: never commit it or publish it.

Throughout this skill, `<Name>`, `<CV folder>` and the other placeholders below come from the profile.

## Step 1: Guided intake (always first, before any research)

If the inputs below weren't all given as args, send ONE message with this fill-in checklist and wait for the reply. Pre-fill anything already known:
- args;
- the profile;
- `runs/<company>-<role>.md`, if one exists for this role. In that case, only ask what changed, e.g. a new stage or interviewer.

```
To prep, fill in (defaults in [brackets]; reply "ok" to keep them):
1. Company:
2. Role title:
3. JD URL:
4. Tailored CV: [<CV folder>/<tailored CV pattern with Company filled in>]
5. Generic CV: [<CV folder>/<generic CV>]
6. Interviewer name + LinkedIn URL:
7. Interview stage: [recruiter screen]  (recruiter / hiring manager / panel / case / final)
8. Most recent salary: [<from profile>]
9. Anything else relevant for this role? e.g. referral, notes from earlier conversations,
   specific team or product, location/visa constraints, timeline, competing offers.
```

Then:
- Find the tailored CV in the CV folder with `ls`. On macOS, `mdfind -name` also works. If there's no match, ask which file to use. If there's no tailored CV, use the generic one.
- Re-ask any missing required field (1, 2, 3, 6) before researching.
- Echo all inputs back in one line, then proceed.
- Save the inputs to `runs/<company>-<role-slug>.md` in this skill's folder (see Step 6). Run files are private.

## Step 2: Create the doc skeleton first
Create a Claude Doc titled `<Company> – <Role>: <Stage> Prep`, with a byline (date · me) and one `pending` block per section in the template below. Open it, then fill it section by section as research lands.

## Step 3: Read inputs (in parallel)
- Read the CVs (Read tool on the PDFs).
- WebFetch the JD: responsibilities, requirements, values, location, salary and benefits.
- **Answer bank (optional):** if the profile lists one, read it fresh every run, because the user keeps adding to it.
  - It may be a Notion database or page, a doc, or a local file.
  - For a Notion database, query the view, then fetch the **pitch** entry in full, plus any entries whose name, tags or summary match the JD.
  - Bank content beats CV wording where they differ, but numbers must still match the CV.
  - If the bank can't be read (no connector, or the fetch fails), say so in one line and fall back to the CVs.

## Step 4: Research (send searches in parallel; see `references/sources.md`)
1. **Mission and money:**
   - Filings: UK → Companies House (company number, accounts type and date, officers, charges); US → SEC 10-K/10-Q; elsewhere → the national company registry.
   - Mission, top 3 strategic priorities (mark them *inferred*), who the customer is (B2C / B2B / B2B2C), and culture/values.
2. **Competitors:**
   - FIRST establish which markets the company operates in and how much each matters.
   - Label every competitor by market: **domestic** (name the country), **international** (name the markets), or software/platform (with markets).
   - Rank them by relevance to the company's main markets. Keep the top ~5 in a table: Competitor | Market(s) | How <Company> differs.
   - End with a one-line moat.
3. **AI strategy:** AI/ML features, the stack (inferred from engineering/data job ads), the engineering blog, and papers or talks. Mark inferences.
4. **Recent moves (last 6 months from today):** hires, partnerships or acquisitions, launches or new markets, funding, and leadership changes. Check the company newsroom and trade press.
5. **Interviewer:** LinkedIn plus a web search. If the www URL redirects, try the country subdomain, e.g. `uk.linkedin.com/in/<handle>`.
   - Identify their function (TA vs product vs exec), because it decides the brief's emphasis.
   - Use they/them unless their pronouns are stated.
6. **Salary:** a company-published band, local salary benchmarks, recruiter ads for comparable roles, and Glassdoor/Levels.fyi.
   - Anchor above the current salary given fit, and give an ask, a range, a floor and a script.

Always open the page a number comes from (snippets aren't sources), and label unverified figures.

## Step 5: Write the brief (template)
Sections, in order. Use bullets, not prose, and keep each section to its takeaways:
- **First line under the byline:** `**JD:** [<Role> at <Company>](<JD URL>)`. Link the clean JD URL, with tracking parameters like `?_gl=`, `gclid` and `gbraid` removed.
- **Then, with no heading:** a numbered list of three quoted answers in the user's voice, in this order:
  1. **Why <Company>?** ONE line, heavy on the company's mission, its values (use their own value words where natural) and its differentiator versus competitors.
  2. **Why this role?** 1–2 lines on what the role owns, why now for the company, and how it connects to the user's recent experience.
  3. **Why me (pitch):** this doubles as the 60–90s "tell me about yourself" story, so there's no separate story section.
     - **Baseline:** the bank's pitch entry if there is one, otherwise the CV profile.
     - Keep its structure and voice, and tailor it to the JD: reorder or emphasise the points the JD cares about, swap in the most relevant proof points and numbers, and end with a role-specific closing line.
     - Don't invent new claims.
     - Under it, add a short nested list of 3 core strengths.
  Use only sourced facts, and no unverified figures.
- **1. <Company> at a glance:**
  - What it does, and its customers.
  - **Mission (verbatim):** the company's own mission statement in quotes, copied word for word from a page you opened (e.g. its about or careers page) and linked. If none exists, say so instead of paraphrasing.
  - Priorities, money (add a to-do if the accounts weren't read) and culture.
- **2. My fit:**
  - **Edge:** start from the pitch points, mapped to the JD requirements one by one.
  - **Gap:** the gap, with an answer.
  - **"If asked about… / Use" table (4 rows):** where a bank answer or story fits a row, name it and link it in the "Use" column instead of rewriting it.
  - Don't repeat the pitch here.
- **3. Competitors:** a markets line, the table and the moat line.
- **4. AI, data and recent moves.**
- **5. Interviewer.**
- **6. Salary:** the ask, range and floor in bold, then benchmarks and a script.
- **7. Questions to ask:** always start with these 4 default questions, word for word, with <Company> filled in:
  1. What would success look like in this role?
  2. What's something people who thrive here do differently from those who struggle?
  3. What's the biggest challenge/opportunity <Company> is currently facing?
  4. What would success look like in the role in the first 3–6 months?

  Then add 2–3 tailored questions, based on the role, the company's recent moves and the interviewer's function, plus one logistics line.

**Stage switch:**
- **Recruiter:** breadth, fit, logistics and salary.
- **Hiring manager or panel:** add a "Likely product case" section (2–3 prompts, each with an answer outline), and cut salary to 2 lines.
- **Final:** add a 30/60/90 plan, and cut competitors to 3 rows.

## Step 6: Length check and save
- Export the tab as an A4 PDF with the docs `export` tool.
  - The result is large, so decode it with `grep -o 'JVBERi[A-Za-z0-9+/=]*' <saved file> | head -1 | base64 -D > <scratchpad>/brief.pdf` (use `base64 -d` on Linux), then Read it.
  - If it's over 3 pages, trim (merge bullets, shorten table cells, drop repeats) and re-check.
- Update the run file `runs/<company>-<role-slug>.md` with the date, all intake inputs, the extra context, the doc link and open to-dos.
- Final chat reply: one line with the doc link and the open to-dos.
