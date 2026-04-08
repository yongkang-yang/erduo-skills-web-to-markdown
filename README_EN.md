

## 🔗 Web To Markdown

```bash
npx skills add rookie-ricardo/erduo-skills --skill web-to-markdown
```

Routes each URL to a source-aware extraction strategy and returns clean markdown for downstream agent tasks such as summarization, translation, and review.

- General pages and X/Twitter use `r.jina.ai` by default
- YouTube URLs use `defuddle.md` for transcript-oriented extraction
- WeChat, Zhihu, and Feishu use `cuimp` Chrome-impersonated HTTP fetching, then auto-fallback to browser extraction when needed
- Built-in generic fallback chain: if `r.jina.ai` fails, try direct fetch + Mozilla Readability, then browser extraction
- Supports `--json` metadata output (`strategy`, `source`, normalized URL, and markdown)

```bash
cd skills/web-to-markdown
npm install
node scripts/url_to_markdown.mjs <url>
node scripts/url_to_markdown.mjs <url> --json
```

---

## 🖼 Gemini Watermark Remover

```bash
npx skills add rookie-ricardo/erduo-skills --skill gemini-watermark-remover
```

Removes the visible Gemini AI watermark from the bottom-right corner of generated images using reverse alpha blending. Pixel-perfect restoration.

- Pure Python, only depends on Pillow
- Pre-captured alpha masks: 48px (small images) / 96px (images >1024×1024)
- Algorithm: `original = (watermarked - alpha × logo) / (1 - alpha)`

```bash
python skills/gemini-watermark-remover/scripts/remove_watermark.py <input-image> <output-image>
```

For algorithm details, see `skills/gemini-watermark-remover/references/algorithm.md`

---

## 📂 Project Structure

```
erduo-skills/
├── .claude/
│   └── agents/                     # Agent definitions
├── skills/
│   ├── daily-news-report/          # Daily News Report
│   │   ├── SKILL.md
│   │   ├── sources.json
│   │   └── cache.json
│   ├── ak-rss-digest/             # RSS Digest
│   │   ├── SKILL.md
│   │   ├── scripts/
│   │   └── references/feeds.opml
│   ├── transcript-polisher/        # Transcript Polisher
│   │   ├── SKILL.md
│   │   └── references/
│   ├── translate-polisher/         # Translate Polisher
│   │   ├── SKILL.md
│   │   └── references/
│   ├── web-to-markdown/            # Web To Markdown
│   │   ├── SKILL.md
│   │   ├── scripts/
│   │   └── references/
│   └── gemini-watermark-remover/   # Gemini Watermark Remover
│       ├── SKILL.md
│       ├── scripts/
│       ├── assets/
│       └── references/
├── NewsReport/                     # Generated report archive
├── README.md                       # Documentation (Chinese)
└── README_EN.md                    # Documentation (English)
```

## Claude Code Installation Supplement

This repository can be registered as a Claude Code plugin marketplace.

### Native Claude Code Commands

Add the marketplace:

```bash
/plugin marketplace add rookie-ricardo/erduo-skills
```

Then install the plugin bundle you want:

```bash
/plugin install research-workflows@erduo-skills
/plugin install writing-workflows@erduo-skills
/plugin install image-tools@erduo-skills
```

Bundle contents:

- `research-workflows`: `ak-rss-digest`, `daily-news-report`
- `writing-workflows`: `transcript-polisher`, `translate-polisher`, `web-to-markdown`
- `image-tools`: `gemini-watermark-remover`

For local testing, use the repository path directly:

```bash
/plugin marketplace add ./
/plugin install research-workflows@erduo-skills
```

If you use the `skills` CLI, you can also add this repository directly:

```bash
npx skills add rookie-ricardo/erduo-skills
```

## 🤝 Contributing

Contributions welcome! Each skill is a self-contained directory under `skills/`, with a `SKILL.md` (skill definition) and related scripts/resources.

[![Star History Chart](https://api.star-history.com/svg?repos=rookie-ricardo/erduo-skills&type=Date)](https://www.star-history.com/#rookie-ricardo/erduo-skills&Date)

---

*Created with ❤️ by Erduo*
