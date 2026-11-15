# Chengdu Environment Group in Australia: market-entry research · 成都环境集团澳洲市场研究

🏆 **NexStar Excellence Award, City of Melbourne** · NexStar 2026 Melbourne–Chengdu Sprint, team CDEG–A
**Live site 网站 → [cdeg.ksmarsh.net](https://cdeg.ksmarsh.net)** (bilingual EN/中文)

## Executive summary
- **Answer:** a two-speed, asset-light entry. CDEG should start now in businesses that need no waste-to-energy (WtE) licence and no equity (sludge and biosolids services, food-waste decontamination, smart water meters for regional utilities), and lead its WtE play with operations and maintenance for existing licence holders.
- **Why:** Victoria's 2.5 Mt/yr thermal WtE cap is already 94% allocated, but none of the licensed plants is built or has named an operator. Their operation is worth about A$176m a year, or A$45–91m after political and self-operation risk.
- **So what:** CDEG's edge is operating experience, not licences. Three licence holders (Cleanaway, HiQ, Melbourne Water) are big enough for its two-line plants.

## Problem
Chengdu Environment Group, a Chinese waste and water company, wants to enter Australia. The team was asked where it can compete, what approvals each business line needs, and whether the economics work.

## Approach
- Desk research across 130+ cited sources (EPA Victoria licences, parliamentary inquiry submissions, utility tenders, company filings). Model inputs live in `data/assumptions.csv`, each with a source ID.
- Business-line analysis (waste-to-energy, sludge, organics, meters, chemicals) and a compliance map of the approvals each line needs.
- **Interactive models (Observable JS):** a WtE plant payback/NPV model for a Latrobe Valley site, an O&M contract model, a meter-distributor model and a council map, all driven by one assumptions table.

## Key findings
![NPV of a Latrobe WtE plant against gate fee](assets/img/report-fig-1.png)
- In the plant model, an owner needs a gate fee of about **A$205/t** (2027 dollars) to break even, and value peaks near **A$240/t**. Metro landfill costs about A$272/t, which sets the ceiling.
- Every 5 points of plant availability is worth about **A$40–45m** to an owner. That's the lever an experienced operator controls.
- Political risk is as large as community risk: 86% of 537 inquiry submissions raise health concerns.
- Chinese entrants have done best as service businesses with local partners (e.g. BEWG's TRILITY). Control of critical networks has been refused.

## Tools
Quarto (bilingual website, custom language toggle) · Observable JS (interactive models) · D3 · KaTeX · GitHub Actions → Aliyun OSS (Hong Kong) → Cloudflare. The site is fully static with no external CDNs, so it loads inside mainland China.

## Repository contents
```
report/       introduction, market context, opportunity, customers, competitors, go-to-market
part-a/       business models, one page per line
part-b/       compliance and approvals
models/       interactive models (Observable JS)
appendix/     sources, assumptions, glossary
data/         assumptions.csv, sources.csv: the single source of numbers
assets/       language toggle, styles, vendored JS
```

## Limitations
- This is a student consulting project based on public sources. Figures marked "to verify" on the site aren't final.
- Model outputs are illustrative and depend on capex, price and landfill-levy assumptions, which swing value more than operations do.

## Team
Kai Marsh · Christine (Kuntong) Jiang · Janeika Jeyakanthan. Section authorship is shown on each page of the site.

---

## For the team: working on the site · 团队协作说明

### How it works · 工作流程

```
edit .qmd → push to main → GitHub Actions runs `quarto render` → _site/ deployed to Aliyun → live at cdeg.ksmarsh.net
修改 .qmd → 推送到 main → GitHub Actions 自动构建 → 部署到阿里云 → 网站更新
```

The site is fully static (no server, no CDN, bundled JS), so it loads inside mainland China.
网站为纯静态（无服务器、无外部 CDN），中国大陆可正常访问。

### Folder layout · 目录结构

```
_quarto.yml   site config, navbar, theme        网站配置、导航栏
index.qmd     home page                         首页
part-a/       business models, one page per line 商业模式（每个业务一页）
part-b/       compliance and approvals           合规与审批
models/       interactive models (Observable JS) 互动模型
appendix/     sources, assumptions, glossary     来源、假设、术语
data/         assumptions.csv, players.csv, sources.csv — the single source of numbers 所有数据的唯一来源
assets/       language toggle, styles, vendor JS 语言切换、样式、本地 JS 库
```

### Editing · 如何编辑

**Small edits 小改动:** open the `.qmd` file on GitHub → pencil icon → edit → *Commit changes*. The site updates in ~2 minutes.
在 GitHub 网页上打开 `.qmd` 文件 → 点铅笔图标 → 修改 → *Commit changes*，约 2 分钟后网站更新。

**Bigger edits 大改动:**

```bash
git clone https://github.com/kyanite03/chengdu-env-market-research.git
cd chengdu-env-market-research
quarto preview        # live preview in browser 浏览器实时预览
git pull              # always pull before pushing 推送前先 pull
git add . && git commit -m "Part A: WtE costs" && git push
```

Install Quarto from https://quarto.org/docs/get-started/ (no R or Python needed 无需 R 或 Python).

### Writing rules · 写作规则

- Write every section twice, in `::: {.en}` and `::: {.zh}` blocks. 每部分写中英两版，分别放在 `::: {.en}` 和 `::: {.zh}` 中。
- Unfinished content → `::: {.placeholder}` (yellow box). 未完成内容 → 黄色占位框。
- Unconfirmed facts → `[to verify]{.verify}` / `[待核实]{.verify}`. 未确认的数据要标注。
- Every number goes in `data/assumptions.csv` with a `source_id` from `data/sources.csv`. 所有数字须录入 `assumptions.csv` 并注明来源。
- Check `quarto preview` before pushing a large change: a broken page breaks the deploy. 大改动推送前先本地预览，构建失败会导致网站无法更新。

### ⚠️ Public repo · 公开仓库

This repository is **public**. Do not commit:
本仓库为**公开**仓库，请勿提交：

- CDEG internal documents, meeting notes, or anything shared with us in confidence 集团内部资料、会议记录或保密信息
- Contact details (phone numbers, emails, WeChat IDs) 联系方式
- Passwords, keys or server details — deploy credentials live only in GitHub *Settings → Secrets* 密码、密钥或服务器信息（部署凭证仅存于 GitHub Secrets）

### Status · 进度

- [x] Skeleton pages and language toggle 页面框架与语言切换
- [x] Hosting and auto-deploy 托管与自动部署
- [x] WtE payback model prototype (illustrative numbers) 垃圾发电回本模型原型
- [ ] Link models to `data/assumptions.csv` 模型接入数据表
- [ ] Part A / Part B content 第一、二部分内容
- [ ] Other models 其他模型

---

NexStar 2026 · CDEG–A · Draft — figures marked "to verify" are not final. 草稿：标注"待核实"的数据尚未确定。
