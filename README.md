[中文版](./README.zh-CN.md)

# bela-content-creator

**A Claude Code plugin for AI content creators** — automates your daily workflow: industry briefing, topic selection, video scripts, and job search briefing, all personalized to your background and platform.

Built by an AI content creator who got tired of spending 2+ hours every morning manually reading news, picking topics, and writing scripts. This plugin runs those workflows inside Claude Code with a single trigger word.

## What It Does

| Skill | What You Say | What You Get |
|-------|-------------|--------------|
| **Daily Briefing** | `日报` / `daily briefing` | Full industry digest — reports, policy, launches, funding |
| **Topic Picker** | `选题` / `video topics` | 3–5 scored topic recommendations ranked by your background and platform |
| **Video Topics** | `视频选题` / `video script` | Topic cards with complete 2-minute monologue scripts |
| **Content Planner** | `onboarding` / `内容规划` | First-run setup: builds your creator profile used by all other skills |
| **Job Briefing** | `求职日报` / `job briefing` | Daily AI PM job search report — 20+ companies, match scoring, P0 actions |

## Who It's For

- AI content creators (short video, newsletter, blog) who cover tech / AI
- Product managers or professionals running a side content channel
- Anyone who wants to reduce daily research overhead and focus on creating

## Background

Most content creator workflows are manual and slow: open 5 tabs, scan Twitter/X, read WeChat posts, copy-paste into a draft. This plugin replaces that with structured, searchable, source-linked briefings that adapt to your specific domain — not generic AI news.

The **Job Briefing** skill is for creators who are also navigating a job search in the AI space — it runs targeted searches across 20+ AI companies, scores each role against your background, and surfaces the P0 actions for the day.

Everything personalizes to a profile you set up on first run. Nothing is hardcoded.

---

## Installation

### Method 1 — Clone directly (recommended)

```bash
git clone https://github.com/belalee-ai/bela-content-creator.git ~/.claude/plugins/bela-content-creator
```

Then restart Claude Code (or run `/reload` if supported). The plugin skills will be available immediately.

### Method 2 — Via Claude Code plugin command

If your Claude Code version supports the `/plugin` command:

```bash
# In Claude Code terminal:
/plugin install https://github.com/belalee-ai/bela-content-creator
```

> Check your Claude Code version for exact syntax. Plugin installation commands may vary across releases.

### Method 3 — Superpowers / third-party plugin managers

If you use the [Superpowers plugin system](https://github.com/anthropics/claude-code), you can install from within Claude Code:

```
/find-skills bela-content-creator
```

Or add this repo as a plugin source and install from the skill browser.

### Method 4 — Manual copy (no git required)

1. Download the ZIP: **[belalee-ai/bela-content-creator → Code → Download ZIP](https://github.com/belalee-ai/bela-content-creator/archive/refs/heads/main.zip)**
2. Unzip and copy the folder to `~/.claude/plugins/bela-content-creator/`
3. Restart Claude Code

---

## Quick Start

1. Install using any method above
2. Open Claude Code in any project directory
3. Type a trigger word: `日报`, `选题`, or `求职日报`
4. First run: a 5-question onboarding builds your creator profile (~2 minutes)
5. Every subsequent run uses your profile — no repeated setup

**Update your profile anytime:** say `update my profile` or `更新我的创作者设置`

---

## Privacy

Your creator profile and job search profile are stored **locally only** in `shared/` within your working directory. This directory is gitignored — it is never committed or synced to any remote.

The plugin has no network calls of its own. All searches run through Claude Code's built-in web search.

---

## Structure

```
.claude-plugin/
  plugin.json          # Plugin manifest
skills/
  daily-briefing/      # Industry digest
  topic-picker/        # Scored topic recommendations
  video-topics/        # Topic cards + scripts
    references/
      compliance-rules.md
  content-planner/     # Onboarding + profile router
  job-briefing/        # AI PM job search briefing (6 modes)
    references/
      search-sources.md       # Company lists + search templates by industry
    templates/
      daily-job-report.md     # Output template
      user-profile-template.md
      bookmarks-template.md
creator-profile.template.md   # Unified profile template (copy to shared/)
```
