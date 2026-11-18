# interview-prep: a Claude Code skill

Type `/interview-prep` in Claude Code to get a research-backed interview brief of at most 3 A4 pages, written as a Claude Doc.

## What the brief covers
- **Why this company, why this role, why me:** your pitch, tailored to the job description.
- **Company at a glance:** what it does, its customers, its mission (quoted verbatim), its priorities, its finances (from company filings) and its culture.
- **Your fit:** your edge mapped to the job description, your gaps and how to answer them, and an "If asked about…" table.
- **Competitors:** grouped by market (domestic vs international), with how the company differs from each.
- **AI and data strategy,** plus the company's moves in the last 6 months.
- **Interviewer profile:** their function decides what the brief emphasises.
- **Salary:** an ask, a range and a floor, with benchmarks and a script.
- **Questions to ask:** 4 default questions plus tailored ones.

The brief adapts to the interview stage (recruiter, hiring manager or panel, final).

## Install
```
git clone https://github.com/<your-username>/interview-prep-skill ~/.claude/skills/interview-prep
```
You can also download the ZIP and put the folder at `~/.claude/skills/interview-prep/`.

## Requirements
- [Claude Code](https://claude.com/claude-code).
- The **Claude Docs** connector, which the brief is written in.
- Web search and fetch, used for the research.
- Optional: a **Notion** connector, or another connector, if your answer bank lives there.

## First run
Run `/interview-prep`. The first time, Claude asks for your profile and saves it to `profile.md`, which is git-ignored. See `profile.example.md` for the fields: your name, CV folder, CV file names, current salary and an optional answer bank.

After that, each run asks for the role details:
- company and role title
- the job description link
- which CVs to use
- the interviewer
- the interview stage
- your salary
- any extra context

Each run's inputs and doc link are saved in `runs/`, which is also git-ignored, so you can reuse them for later stages of the same role.

## Answer bank (optional, recommended)
Keep your reusable answers and stories in one place, such as a Notion database, and add its link to your profile. The skill reads it fresh on every run. It uses your **pitch** entry as the starting point for "Why me" and links your stories in the brief rather than rewriting them.

## Privacy
Your profile, salary, CVs and run notes stay on your machine. `profile.md` and `runs/` are git-ignored, so don't commit them.
