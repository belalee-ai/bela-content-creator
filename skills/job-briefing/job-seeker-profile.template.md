# Job Seeker Profile Template

Copy this file to `shared/job-seeker-profile.md` and fill in your details.
The `shared/` directory is gitignored — your data stays local.

```yaml
background:
  companies:
    - company: "前公司A"
      role: "产品经理"
      focus: "增长、广告投放、核心指标"
    - company: "前公司B"
      role: "产品经理"
      focus: "会员体系、订阅商业化"
  years_of_experience: 5

target:
  city: "上海"
  industry: "AI / 大模型"
  role: "产品经理"
  level: "P6-P8"  # 或 senior / staff / principal
  job_type: "社招"

strengths:
  - "增长产品思维（漏斗分析、A/B 实验）"
  - "商业化产品经验（会员/订阅/广告）"
  - "AI 工具深度使用与产品感知"
  # 在此补充你的差异化能力

salary_filter:
  enabled: false  # true = 低于预期的岗位降权排序
  min_base: null  # 如 "30k"
```
