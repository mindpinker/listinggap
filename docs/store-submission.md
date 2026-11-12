# Chrome Web Store 提交包

**产品**：ListingGap  
**版本**：1.0.0 公开；1.0.1 审核中  
**模式**：免费、纯本地、无账号、无付费墙  
**日期**：2026-11-06

> **名称检查已完成第一轮。** CWS 精确搜索未发现同名；"Listing Doctor" 已被两个插件占用，
> 不可使用。USPTO / EUIPO / WIPO 尚未完成（均有验证码），付费推广前必须由律师复核。
> 记录见 `docs/trademark-check.md`。

## 0. 实际提交记录

2026-11-06 提交审核；2026-11-12 在开发者后台确认已公开发布。

2026-11-12 上传 1.0.1（反馈入口、Amazon 登录墙检测、复制/导出后的评价提示），状态：待审核。

| 项目 | 值 |
|---|---|
| 商品 ID | `jdmmcbmgmhhjcblaefgmofllhaodafkg` |
| 状态 | **已发布 - 公开发布**（Published — public） |
| 当前用户数 | 2 |
| 当前评分 | 暂无评分 |
| 审核通过后自动发布 | 已勾选 |
| 收费模式 | 免费，无应用内购 |
| 公开范围 | 公开 |
| 分发地区 | 所有地区，**排除中国** |
| 类别 | 工作流程与规划（Workflow & Planning） |
| 语言 | 英语（美国） |
| 商店图标 | 128×128，已上传 |
| 截图 | 5 张 1280×800，已上传 |
| 首页 URL | https://mindpinker.github.io/listinggap/ |
| 隐私政策 URL | https://mindpinker.github.io/listinggap/privacy.html |
| 支持 URL | https://mindpinker.github.io/listinggap/#support |
| 数据披露 | 网站内容；无远程代码；三项确认已勾选 |
| 权限理由 | activeTab / storage / sidePanel / Amazon 主机权限均已填写 |

开发者后台：

```text
https://chrome.google.com/webstore/devconsole/314b6557-d5a4-40dd-b929-f71a5964c4e5/jdmmcbmgmhhjcblaefgmofllhaodafkg
```

公开商店 URL：

```text
https://chromewebstore.google.com/detail/jdmmcbmgmhhjcblaefgmofllhaodafkg
```

已公开发布。当前从中国/香港网络访问公开页可能显示“不可用”，因为分发地区排除了中国；请用美国/欧洲 IP 或无痕窗口验证公开页。

状态截图：`docs/screenshots/cws-pending-review.png`

## 1. 商店名称与文案

### 推荐标题

**ListingGap — Amazon Listing Audit & Rewrite**（43 字符，低于 CWS 的 45 字符上限）

备选（如果标题超限或商标冲突）：

- **ListingGap — Find Unanswered Buyer Objections**
- **ListingGap — Review-to-Listing Rewrite**

### 短描述（132 字符以内）

> Find the buyer objections your Amazon title and bullets never answer, then get an evidence-backed rewrite. Free and local.

### 详细描述

```text
Your reviews already explain why the page does not convert. ListingGap turns those complaints into a listing rewrite you can actually use.

Open an Amazon product page, click Audit, and ListingGap will:

• Read the title, bullets, description, A+ presence, rating, images, Q&A, and Amazon's "Customers say" summary.
• Find recurring buyer objections, prioritizing 1–3 star reviews.
• Show which objections your title and bullets answer, partly answer, or never mention.
• Flag claims that buyers' own words contradict.
• Rewrite the title within the marketplace limit, plus five bullets and an A+ outline.
• Mark missing facts as [Needs input] instead of inventing materials, certifications, or test results.
• Export Markdown or CSV, copy individual blocks, and keep up to 20 audits locally.

FREE — NOT A TRIAL
Every feature is free. There is no account, no credits, no license key, and no upsell. The analysis engine runs inside the extension, so there is no per-audit server cost.

PRIVATE BY DESIGN
No backend. No analytics. No tracking. No remote AI. Listing and review text stays in your browser. Review-page requests go only to the Amazon domain you are already visiting. Saved audits use local browser storage and can be cleared at any time.

WHEN REVIEWS ARE HIDDEN
Amazon often hides low-star review bodies. ListingGap uses visible reviews, the "Customers say" summary, critical review pages, and a manual paste/CSV fallback. If evidence is thin, it says so instead of guessing.

WHAT IT DOES NOT DO
No keyword search volume, sales estimates, PPC automation, image generation, or fake-review detection. It is a focused listing audit, not a replacement for a full research suite.

ListingGap is an independent tool. It is not affiliated with, endorsed by, or sponsored by Amazon. Verify every claim before publishing.
```

### 分类

- 主分类：Productivity
- 次分类（如可选）：Business tools

### 语言

- 界面：English
- 商店文案：English

## 2. 单一用途说明

**Single purpose statement**

> ListingGap audits the Amazon product page the user is viewing and rewrites its title and bullets so they answer objections found in the listing's reviews.

这个说明必须能覆盖所有功能：提取 Listing、读取评论、异议地图、缺口检查、重写、证明缺口、复制/导出、历史。不要把它描述成"Amazon 卖家全能工具"。

## 3. 权限理由

在 CWS 的权限说明里逐项填写，不要只写"为了功能"。

| 权限 | 提交说明 |
|---|---|
| `activeTab` | "Reads the Amazon listing the user explicitly chooses to audit. The extension does not read other tabs." |
| `storage` | "Stores the user's title-limit preference and up to 20 recent audits locally with chrome.storage.local. Nothing is synced or uploaded." |
| `sidePanel` | "Displays the audit report beside the Amazon page so the user can compare the report with the listing." |
| Amazon host permissions | "Reads the current Amazon product page and requests review pages for the same ASIN from the same Amazon marketplace. No non-Amazon host is requested." |

**不要添加**：

- `scripting`
- `<all_urls>`
- `tabs`
- `windows`
- `cookies`
- `webRequest`

## 4. 数据使用披露

建议在 CWS 隐私表单中按以下口径填写：

| 问题 | 回答 |
|---|---|
| Does the extension collect personally identifiable information? | No |
| Does it collect health, financial, authentication, personal communications, location, or web history? | No |
| Does it collect website content? | It processes Amazon listing/review text locally; it is not transmitted to the developer or a third party. Review-page requests go to Amazon. |
| Is data sold to third parties? | No |
| Is data used for purposes unrelated to the single purpose? | No |
| Is data used for creditworthiness or lending? | No |
| Is remote code loaded? | No. All analysis code is packaged with the extension. |
| Does it use analytics or tracking? | No |

隐私政策公开 URL 必须可访问。可以把 `extension/privacy.html` 和 `extension/sidepanel.css` 一起部署到 GitHub Pages、Cloudflare Pages 或自有域名（页面依赖这份样式表），例如：

```text
https://<your-domain>/listinggap/privacy.html
```

**不要**把 `chrome-extension://` 地址填进 CWS 的隐私政策字段。

## 5. 截图与素材

Chrome Web Store 截图必须是 **1280×800** 或 **640×400**。项目内的 430×1000 侧栏截图只用于开发 QA，不能直接上架。

推荐 5 张 1280×800：

1. **Report** — 分数、四项权重、Top objections。标题："See what the page never answers."
2. **Objections** — "Your listing says / Buyers say" 对比。标题："Every objection has a receipt."
3. **Rewrite** — 标题 + 五条重写 + `[Needs input]` 标记。标题："Paste-ready copy, not generic AI filler."
4. **Proof gaps** — "leak proof" 被评论反驳。标题："Catch claims buyers already contradict."
5. **Privacy/local** — 设置抽屉或隐私页。标题："Free. Local. No account. No API key."

可选宣传图：440×280 或 920×680。文案保持同一句价值主张，不要放亚马逊官方 logo 或暗示官方背书。

## 6. 提交前检查清单

- [ ] 搜索 CWS 精确名称和近似名；确认无同名/混淆。
- [ ] 查 USPTO TESS；如面向欧洲/全球，查 EUIPO 和 WIPO。
- [ ] 确认域名/支持邮箱可用。
- [ ] `manifest.json` 的 `name`、商店标题、隐私页品牌名一致。
- [ ] `manifest.json` description 不超过 132 字符。
- [ ] 运行 `npm test`，全部通过。
- [ ] 运行 `node scripts/verify-extension.cjs`，报告 `ok: true`。
- [ ] 运行 `npm run package`，生成 `dist/listinggap-v1.0.0.zip`。
- [ ] 解压 zip 到临时目录，用 Chrome 加载解压后的目录，确认能打开侧栏。
- [ ] 在至少 3 个真实 Amazon ASIN 上测试：有 A+、无 A+、低星评论被隐藏。
- [ ] 确认评论被限流时出现可理解的错误/证据不足状态，而不是空白或假数据。
- [ ] 确认粘贴评论、CSV 导入、Markdown/CSV 导出、清除历史都可用。
- [ ] 隐私政策已部署到公开 HTTPS URL。
- [ ] 商店描述包含 "not affiliated with Amazon"。
- [ ] 截图是 1280×800/640×400，且不含真实个人信息。
- [ ] 没有付费、试用、license key、外部 AI 调用或远程代码。

## 7. 审核备注模板

```text
ListingGap is a single-purpose Amazon listing audit tool. The user opens an Amazon product page and clicks the toolbar icon. The side panel reads that page and its reviews, then displays objections, listing gaps, and a suggested rewrite.

The extension has no backend and makes no requests to the developer. Review-page requests go only to the same Amazon marketplace the user is visiting. All analysis runs locally. No remote code is loaded.

To test without an Amazon account:
1. Open any public Amazon product page.
2. Click the ListingGap icon.
3. Click "Audit this page".
4. If Amazon limits review access, open "Reviews hidden? Paste them here" and paste reviews in the format "2|The clasp broke after two wears."

The demo fixture is available at chrome-extension://<id>/sidepanel.html?demo=1 after loading the unpacked extension.
```

## 8. 上架后第一周

- 监控侧栏错误：DOM 选择器失效、评论页 403/验证码、存储配额。
- 收集用户粘贴评论的原因，判断是 Amazon 隐藏、登录墙还是选择器问题。
- 不承诺"提升销量"或"提高排名"；用"发现未回答的异议"和"生成可验证的改写"作为结果指标。
- 如果收到名称/商标异议，立即准备备选名并统一改 manifest、商店标题、隐私页和落地页。
