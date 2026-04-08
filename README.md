
---

## 🔗 Web To Markdown

```bash
npx skills add rookie-ricardo/erduo-skills --skill web-to-markdown
```

将 URL 按站点类型路由到对应抓取策略，统一输出可读 Markdown，适合给后续 Agent 继续分析、翻译或摘要。

- 通用网页与 X/Twitter 默认走 `r.jina.ai`
- YouTube 链接走 `defuddle.md` 提取字幕/正文
- 微信公众号、知乎、飞书走 `cuimp` Chrome 指纹 HTTP 抓取，失败时自动降级浏览器提取
- 内置通用兜底链路：`r.jina.ai` 失败后会尝试直连抓取 + Mozilla Readability，再尝试浏览器提取
- 支持 `--json` 输出策略、来源与归一化 URL 等元数据

```bash
cd skills/web-to-markdown
npm install
node scripts/url_to_markdown.mjs <url>
node scripts/url_to_markdown.mjs <url> --json
```

