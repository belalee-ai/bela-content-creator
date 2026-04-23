[English](./README.md)

# bela-content-creator

**面向 AI 内容创作者的 Claude Code 插件** — 自动化你每天的内容工作流：行业日报、选题推荐、视频脚本、求职日报，全部根据你的背景和平台定制。

作者是一位 AI 内容博主，厌倦了每天早上手动花 2 小时读资讯、挑选题、写脚本。这个插件把这些工作流搬进了 Claude Code，一个触发词搞定。

## 功能概览

| Skill | 触发词 | 输出内容 |
|-------|--------|----------|
| **每日日报** | `日报` / `每日资讯` / `daily briefing` | 全景行业日报：报告、政策、融资、产品动态 |
| **选题推荐** | `选题` / `视频选题` | 3–5 个评分排序的选题，结合你的背景和平台 |
| **视频选题** | `视频选题` / `口播脚本` | 选题卡 + 完整 2 分钟口播脚本 |
| **内容规划** | `onboarding` / `内容规划` | 首次使用引导：建立创作者画像，供其他 skill 读取 |
| **求职日报** | `求职日报` / `今天有什么岗位` | 每日 AI PM 岗位搜索：20+ 家公司、匹配度评分、今日行动项 |

## 适合谁用

- 做 AI / 科技方向内容的短视频博主、公众号作者、Newsletter 写作者
- 有副业内容创作的产品经理或职场人
- 想减少每日信息收集时间、把精力放在创作上的人

## 背景

大多数创作者的日常工作流都是手动且低效的：开 5 个 tab、刷 Twitter/X、看微信公众号、复制粘贴整理。这个插件用结构化、有来源链接的日报取代了这个流程，且内容根据你的具体领域动态生成，不是泛泛的 AI 资讯汇总。

**求职日报** skill 面向同时在找 AI 方向岗位的创作者——它每天搜索 20+ 家 AI 公司的 PM 岗位，对每个岗位打分，并给出当天的 P0 行动项。

所有内容根据你首次运行时设置的画像个性化生成，没有任何硬编码。

---

## 安装方式

### 方式一 — 直接 clone（推荐）

```bash
git clone https://github.com/belalee-ai/bela-content-creator.git ~/.claude/plugins/bela-content-creator
```

重启 Claude Code（或运行 `/reload`），插件的所有 skill 立即可用。

### 方式二 — 通过 Claude Code 插件命令安装

如果你的 Claude Code 版本支持 `/plugin` 命令：

```bash
# 在 Claude Code 终端中输入：
/plugin install https://github.com/belalee-ai/bela-content-creator
```

> 具体语法因 Claude Code 版本不同可能有差异，请以当前版本文档为准。

### 方式三 — 通过 Superpowers / 第三方 skill 管理器

如果你已安装 [Superpowers 插件系统](https://github.com/anthropics/claude-code)，可以在 Claude Code 中直接搜索安装：

```
/find-skills bela-content-creator
```

或将本仓库添加为插件源，通过 skill 浏览器安装。

### 方式四 — 手动下载（无需 git）

1. 下载 ZIP：**[点击这里下载](https://github.com/belalee-ai/bela-content-creator/archive/refs/heads/main.zip)**
2. 解压后，将文件夹复制到 `~/.claude/plugins/bela-content-creator/`
3. 重启 Claude Code

---

## 快速上手

1. 用上面任意方式安装
2. 在任意项目目录打开 Claude Code
3. 输入触发词：`日报`、`选题` 或 `求职日报`
4. 首次运行：5 个问题建立你的创作者画像（约 2 分钟）
5. 此后每次运行都使用你的画像，无需重复设置

**随时更新画像：** 说 `update my profile` 或 `更新我的创作者设置`

---

## 隐私说明

你的创作者画像和求职画像**只存在本地**，保存在工作目录下的 `shared/` 文件夹中。该目录已加入 `.gitignore`，永远不会被提交或同步到远端。

插件本身不发起任何网络请求，所有搜索通过 Claude Code 内置的网络搜索功能执行。

---

## 目录结构

```
.claude-plugin/
  plugin.json                # 插件元信息
skills/
  daily-briefing/            # 行业日报
  topic-picker/              # 选题推荐
  video-topics/              # 视频选题 + 脚本
    references/
      compliance-rules.md    # 合规红线（国内工具推荐限制）
  content-planner/           # Onboarding + 画像路由器
  job-briefing/              # AI PM 求职日报（6 种运行模式）
    references/
      search-sources.md            # 各行业公司清单 + 搜索词模板
    templates/
      daily-job-report.md          # 日报输出模板
      user-profile-template.md     # 求职画像模板
      bookmarks-template.md        # 岗位标记模板
creator-profile.template.md       # 统一画像模板（复制到 shared/ 填写即可）
```
