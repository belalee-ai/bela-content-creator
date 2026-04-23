[中文版](./README.zh-CN.md)

# bela-content-creator

I used to spend two hours every morning before I could actually start creating: scan the news, figure out what to cover, draft a script outline, check if there's a job worth applying for. All of it manual, all of it repetitive.

This is a Claude Code plugin that does those four things for you. One trigger word, and it runs the whole workflow — searches, summarizes, scores, and writes — based on a profile it builds from you the first time you use it.

---

## What's inside

**Daily Briefing** — say `日报` or `daily briefing`

Searches across your domain and pulls together a structured digest: industry reports, funding news, product launches, policy moves. Organized by category, every item has a source link and a credibility rating. Not a link dump — an actual briefing you can read in 5 minutes.

**Topic Picker** — say `选题` or `video topics`

Takes your background and platform into account and surfaces 3–5 topic ideas, each with a score and a reason. If you want a script too, ask for one — it'll write a 2-minute monologue in your style.

**Job Briefing** — say `求职日报` or `job briefing`

Searches 20+ AI companies for open PM roles, scores each one against your experience, and tells you which ones to act on today. Tracks the ones you bookmark across sessions.

**Content Planner** — say `onboarding`

First-run setup. Asks you 5 questions about your domain, platforms, background, and production constraints. Saves a local profile that every other skill reads from. Takes about 2 minutes.

---

## How it knows about you

First time you use any skill, it walks you through a short setup and saves a profile to `shared/creator-profile.md` — a local file that never leaves your machine. Every search query, every scoring decision, every script it writes is based on that profile.

Say `update my profile` anytime to change your settings.

---

## Install

```bash
git clone https://github.com/belalee-ai/bela-content-creator.git ~/.claude/plugins/bela-content-creator
```

Restart Claude Code. Done.

**Other ways to install**

- `/plugin install https://github.com/belalee-ai/bela-content-creator` — if your Claude Code version supports it
- `/find-skills bela-content-creator` — if you have Superpowers installed
- [Download ZIP](https://github.com/belalee-ai/bela-content-creator/archive/refs/heads/main.zip), unzip to `~/.claude/plugins/bela-content-creator/`, restart

---

## Privacy

Your profile lives in `shared/` inside your working directory. That folder is in `.gitignore` — it won't be committed or synced anywhere. The plugin itself makes no network calls; all searches go through Claude Code's built-in web search.

---

## Repo layout

```
.claude-plugin/plugin.json        version, keywords, author
skills/
  daily-briefing/SKILL.md         industry digest
  topic-picker/SKILL.md           scored topic recommendations
  video-topics/SKILL.md           topic cards + monologue scripts
    references/compliance-rules.md
  content-planner/SKILL.md        first-run profile setup
  job-briefing/SKILL.md           AI PM job search (6 modes)
    references/search-sources.md  company lists by industry
    templates/                    output templates
creator-profile.template.md       copy this to shared/ and fill in
```
