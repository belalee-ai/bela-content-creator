---
name: topic-picker
description: >
  Content topic recommendations with optional video scripts for creators.
  Use when the user says "选题", "topic", "给我找选题", "这周发什么",
  "视频选题", "脚本", "video topics", "give me scripts", "what should I post",
  "content ideas", "内容规划", or "what should I film". First use asks about
  output preferences (format, frequency, scripts). Subsequent runs follow
  saved preferences.
---

# Topic Picker

Generate scored topic recommendations, optionally with ready-to-use scripts. Personalized to the creator's domain, background, platform, and production constraints.

## First-Use Setup

### Step A: Creator Profile

Read `shared/creator-profile.md`. If it does not exist, create it by asking:

1. **What domain do you cover?** (e.g., AI, crypto, indie hacking, marketing tech, design tools)
2. **What's your professional background?** Career experiences and unique skills that differentiate your content.
3. **What platforms do you publish on?** Primary + secondary. Formats? (short video, long-form, image-text, newsletter)
4. **Which regions' news matter to you?** Domestic only / international only / both
5. **What language should output be in?** (中文 / English / bilingual)
6. **Production constraints?** Max video duration, editing skill level, any collaborators who can help.

Save to `shared/creator-profile.md` as structured YAML. Mark `onboarding_complete: true`.

### Step B: Output Preferences

After the profile is set (or on first run of this skill if the profile already exists), ask:

1. **Output format: do you want briefing and topics in one file or separate?**
   - Combined = one file with info digest on top + topic recommendations below
   - Separate = this skill only outputs topic recommendations (use daily-briefing separately for news)

2. **Topic selection frequency?**
   - (a) Every 1-3 days — lighter, fewer topics per run (2-3 topics)
   - (b) Weekly — deeper, more topics per run (4-6 topics)

3. **Do you want full scripts included?**
   - Yes → each topic gets a complete script matching your production constraints (duration, style)
   - No → topic cards only (title, outline, angle, competition status)

Save these preferences to `shared/topic-preferences.md`. On subsequent runs, follow saved preferences without re-asking. User can say "change my output preferences" to reconfigure.

## Search Logic

Build all search queries dynamically from the profile. **No hardcoded search terms, platform names, or company names.**

### Information Gathering

Read `profile.domain` and `profile.news_sources`:

**Template — international (3-5 searches):**
- `"[domain] news this week"` — weekly roundup
- Top companies/products in the domain + `"announcement"` — major moves
- `"[domain] product launch this week"` — new products/tools
- `"[domain] tools trending"` — ecosystem

**Template — domestic (2-4 searches):**
- `"[domain] 本周热点"` or `"[domain] 最新消息"` — roundup
- Key domestic players in the domain + `"最新"` — player moves
- `"[domain] 行业 趋势"` — industry trends

**Auto-feed from briefings:** Also scan the working directory for recent briefing files (last 7 days). Use news items as raw material — abstract each into an evergreen topic idea.

**Evergreen fallback:** When fresh material is thin, generate candidates from the creator's background:
- "[profile.domain] tool comparison" from the creator's use case
- "I tried [tool] for [scenario]" personal experience angles
- "Beginner's guide to [subtopic]" educational content
- "[profile.career] meets [profile.domain]" cross-domain angles

### Competitor Scan

Read `profile.platform.primary` and `profile.platform.secondary`. For each listed platform:

- Search `[platform name] [domain] [keywords] popular` — what's trending
- Search `[platform name] [domain] creator` — who's making content

**Do not scan platforms not listed in the profile.**

Record per candidate: competition density (low/medium/high) + differentiation space + hit content patterns.

## Scoring

Pick up to 8 candidates. Score each against the creator profile.

| Dimension | Weight | Criteria |
|-----------|--------|----------|
| **Audience relevance** | 25% | Does the target audience care? Is it framed around a real user scenario, not an abstract concept? |
| **Unique angle** | 25% | Which specific tag from the creator profile enables a perspective others can't offer? Must name the tag. |
| **Competition** | 20% | Based on actual competitor scan results. Low competition = higher score. |
| **Feasibility** | 15% | Can the creator produce this within their stated constraints? |
| **Growth potential** | 15% | Follower growth, shareability, monetization setup? |

Weighted total = Σ(score × weight), max 5.0.

### Audience Relevance Test

Two hard gates — fail either → score 1, exclude:

1. Does the topic start from a user scenario or an abstract concept? Abstract concept → out.
2. Can a non-expert immediately see "what does this have to do with me"? No → out.

Then:
- Requires unexplained jargon → deduct
- "I saw a [content type] about..." — would a friend say "tell me more" or "what?"

### Filters

- Audience relevance ≤ 2 → exclude regardless of other scores
- High competition + low differentiation → exclude
- Exceeds creator's production constraints → exclude
- Total < 3.0 → exclude
- Max score − min score across candidates must be ≥ 1.5. If all cluster 3-4, re-score.

Sort by score. Take top N based on frequency preference (2-3 for frequent runs, 4-6 for weekly).

## Output

### If preferences say "separate" (topic file only):

Filename: `选题_YYYY年M月D日.md` or `topics_YYYY-MM-DD.md` (per language preference)

Per topic:
- Title + 2-3 alternative titles
- Why this topic, why now
- Content outline (≥ 3 points, each with a concrete action verb)
- Unique angle — citing the specific profile tag
- Competition status from scan
- Production notes
- Score breakdown

If scripts are enabled → append a complete script per topic:
- Length matching `profile.content_constraints.max_duration`
- Style matching `profile.content_constraints.style`
- Visual/format suggestions matching `profile.platform.formats`

End with: competition landscape summary, priority recommendation, excluded candidates with reasons.

### If preferences say "combined" (briefing + topics in one file):

Run the daily-briefing search logic first (see daily-briefing skill for search templates), then topic selection. Output one file with briefing on top and topic recommendations below, separated by a clear divider.

### Script Format (when enabled)

```
[Opening — ~10% of total duration]
(Hook: counterintuitive / data / pain point / suspense)
[2-3 sentences]

---

[Core — ~70% of total duration]
(2-3 points, each a short paragraph)

Point 1: [subheading]
[4-6 sentences]
Visual: [suggestion matching creator's capabilities]

Point 2: [subheading]
[4-6 sentences]
Visual: [suggestion]

---

[Wrap-up — ~20% of total duration]
[Summary + specific engagement prompt]
```

Script rules:
- Total length derived from `profile.content_constraints.max_duration` (e.g., 2 min → ~350 words for Chinese, ~300 words for English)
- Sentence length derived from `profile.content_constraints.style`
- If a script isn't working (hard to explain, no good hook) → swap in a backup candidate. Don't force it.

## Compliance

Read `profile.platform.primary` and `profile.region` (inferred from language/platform choices).

If the creator's region or platform has specific compliance requirements (content labeling rules, tool availability restrictions, sensitive topic policies), note them in a `references/compliance-notes.md` file during onboarding and reference it during topic generation. Do not hardcode any region-specific rules in this skill file.

## Rules

- **No hardcoded search terms.** All queries built from profile fields.
- **No hardcoded platform names in logic.** Platform-specific behavior derived from `profile.platform`.
- **Unique angle must name a specific profile tag.** "From a PM perspective" is too vague.
- **Scores must spread.** Max − min ≥ 1.5.
- **Every source needs a link + credibility marker.**
- **Never fabricate.** Search fails → say so.
- Topics must start from user scenarios, never abstract concepts.
- Filler phrases → concrete facts.
