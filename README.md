# bela-content-creator

Content creator toolkit — daily industry briefing + topic recommendations with optional scripts + AI PM job search briefing.

## Skills

### Daily Briefing
**Triggers:** `日报`、`每日资讯`、`daily briefing`、`today's news`

Full-landscape industry digest for your domain. Covers reports, policy, industry developments, international and domestic news. Pure information — no topic selection.

### Topic Picker
**Triggers:** `选题`、`视频选题`、`脚本`、`topic`、`video topics`、`give me scripts`

Scored topic recommendations tailored to your background and platform. Optionally generates full scripts matching your production constraints.

First use asks 3 setup questions:
1. Output format — combined with briefing or separate file?
2. Frequency — every 1-3 days or weekly?
3. Scripts — include full scripts or topic cards only?

### Video Topics
**Triggers:** `视频选题`、`口播脚本`、`video script`

Full video topic cards with 2-minute monologue scripts. Includes compliance filtering for domestic tool recommendations.

### Content Planner
**Triggers:** `内容规划`、`创作者设置`、`onboarding`、`content plan`

Onboarding router — guides first-time setup of your creator profile (domain, platform, background, production constraints). All other skills read from this profile.

### Job Briefing
**Triggers:** `求职日报`、`job briefing`、`今天有什么岗位`、`职位更新`、`有没有新岗位`

Daily AI PM job search briefing for Shanghai market. Searches 20+ target companies (ByteDance, Ant Group, Xiaohongshu, MiniMax, DeepSeek, Moonshot AI, etc.) for social recruitment PM openings. Outputs:
- Job recommendations with 100-point match scoring
- P0 action items (apply today)
- Industry funding & hiring signals
- Optional job application tracker integration

Tailored to candidates with e-commerce growth (Pinduoduo/TEMU) and subscription monetization (Meitu) backgrounds.

---

## Getting Started

1. Install the plugin
2. Say any trigger word (e.g., "日报", "选题", or "求职日报")
3. First run walks you through a quick profile setup (~1 minute)
4. All subsequent runs are personalized to your domain, platform, and background

## How It Personalizes

The plugin creates `shared/creator-profile.md` on first use, storing your domain, career background, platform strategy, and production constraints. Every search query, scoring decision, and output format is derived from this profile — nothing is hardcoded.

Say "update my profile" anytime to change your settings.

## Job Search Tracking (Optional)

Create `shared/job-tracker.md` to enable persistent job application tracking across daily briefings.
