[English](./README.md)

# bela-content-creator

做内容博主之前，我以为最难的是拍视频。

做了之后才发现，最难的是每天早上——刷完 Twitter、看完公众号、整理完资讯、想完选题，往往已经过了两个小时，还没开始做正事。

这个插件就是为了干掉这两个小时的。

装好之后，在 Claude Code 里说一个词，它帮你搜、帮你整理、帮你打分、帮你写脚本。第一次用的时候回答几个问题，之后每次都按你的情况来，不用重复设置。

---

## 里面有什么

**每日日报** — 说 `日报`

搜你关注领域的最新动态：行业报告、融资、产品发布、政策变化。每条都有来源链接，按类别整理好，不是乱堆一起的链接列表。

**选题推荐** — 说 `选题`

根据你的背景和平台，推 3–5 个选题，每个都有打分和推荐理由。要脚本的话顺便写一篇——2 分钟口播，按你的风格来。

**求职日报** — 说 `求职日报`

每天搜 20 多家 AI 公司的 PM 岗位，对着你的经历打匹配分，告诉你今天该投哪个。你标记过的岗位下次还会继续追踪。

**内容规划** — 说 `onboarding`

第一次使用的引导。问你几个问题：做什么领域、发哪个平台、有什么背景、有什么限制。大概两分钟，之后所有功能都按这个来。

---

## 它怎么知道你是谁

第一次用的时候它会问你，然后把你的回答存到 `shared/creator-profile.md`——一个只存在你本地的文件，不会上传任何地方。之后每次用，它读这个文件，搜索词、打分逻辑、脚本风格都跟着你走。

随时说 `更新我的创作者设置` 可以改。

---

## 安装

```bash
git clone https://github.com/belalee-ai/bela-content-creator.git ~/.claude/plugins/bela-content-creator
```

重启 Claude Code，就好了。

**其他安装方式**

- 在 Claude Code 里输入 `/plugin install https://github.com/belalee-ai/bela-content-creator`（部分版本支持）
- 装了 Superpowers 的话，输入 `/find-skills bela-content-creator`
- [下载 ZIP](https://github.com/belalee-ai/bela-content-creator/archive/refs/heads/main.zip)，解压后拖到 `~/.claude/plugins/bela-content-creator/`，重启

---

## 关于隐私

你的画像保存在工作目录的 `shared/` 文件夹下，已经加了 `.gitignore`，提交代码的时候不会带上去。插件本身不会往外发请求，搜索走的是 Claude Code 自带的联网功能。

---

## 目录结构

```
.claude-plugin/plugin.json        插件信息（版本、关键词）
skills/
  daily-briefing/SKILL.md         每日行业日报
  topic-picker/SKILL.md           选题打分推荐
  video-topics/SKILL.md           视频选题 + 口播脚本
    references/compliance-rules.md 合规红线
  content-planner/SKILL.md        首次设置引导
  job-briefing/SKILL.md           AI PM 求职日报（6 种模式）
    references/search-sources.md  各行业公司清单
    templates/                    日报输出模板
creator-profile.template.md       画像模板，复制到 shared/ 填写
```
