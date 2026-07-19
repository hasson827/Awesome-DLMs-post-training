# Awesome 仓库建设清单（给第一次做 Awesome List 的你）

> 依据 sindresorhus/awesome 官方 manifesto（github.com/sindresorhus/awesome/blob/main/awesome.md）、create-list.md 与主列表 PR 审查实践整理。按顺序逐项完成即可。

## 1. 仓库初始化

- [ ] **仓库名**：`Awesome-<主题>`（连字符命名，如 `Awesome-DLMs-post-training`）。
- [ ] **GitHub Topics**：至少加 `awesome-list`、`awesome`、`list`；再加领域标签如 `diffusion-language-models`、`post-training`、`llm`。
- [ ] **LICENSE = CC0-1.0**：官方 manifesto 推荐公有领域奉献，消除转载/再策展的法律摩擦。备选 CC-BY-4.0；不要用 MIT（语义面向代码），更不要"无 LICENSE"。放置完整 CC0 文本的 `LICENSE` 文件，并在 README 底部加 `## License` 小节。
- [ ] **CONTRIBUTING.md**：主列表收录的硬性要求（本仓库已备好，见 `CONTRIBUTING.md`）。
- [ ] **Code of Conduct**：用 Contributor Covenant v2.1，GitHub 建仓库时一键生成，文件命名 `code-of-conduct.md`。

## 2. README 结构（学术 awesome 推荐骨架）

```markdown
# Awesome-DLMs-post-training [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
> 一句话简介：A curated list of papers on post-training of Diffusion Language Models.

（可选 banner / logo + shields：stars、last-commit、license、PRs-welcome）

## 📰 News        ← 倒序 5–10 条，每条一行含日期；超 10 条折叠进 <details>
## 📑 Contents    ← 目录必须与各级标题完全一致（awesome-lint 会校验）
## 🔍 Scope       ← 明确"什么算 post-training"，最好配一张方法谱系图
## 各分类小节 …
## 🌟 Star History ← star-history.com 嵌入图
## 🤝 Contributing ← 链接到 CONTRIBUTING.md
## 📄 License     ← CC0
```

- [ ] **Awesome 徽章**放在主标题同行：`[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)`。
- [ ] 列表顶部有一段简短的主题描述；推荐右上角放 logo 并链接项目主页。
- [ ] 条目格式两种路线（见第 4 节的取舍）：学术表格风（日期/标题/作者/venue/TL;DR/链接）或标准 `- [Title](url) - Description.` 列表风。

## 3. awesome-lint 与 CI

- [ ] 本地校验：`npx awesome-lint https://github.com/<you>/Awesome-DLMs-post-training`（需 Node.js 20+）。检查项：徽章、列表格式、描述首字母大写且句号结尾、无重复链接、URL 无尾斜杠、ToC 一致性、拼写。
- [ ] CI 工作流 `.github/workflows/lint.yml`：

```yaml
name: Lint
on: [push, pull_request]
jobs:
  lint:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: npx awesome-lint
```

- [ ] **链接存活检查**：加 [lychee-action](https://github.com/lycheeverse/lychee-action)；注意 arXiv 链接常返回 301/302，需配置接受重定向，否则 CI 会误报。
- [ ] PR 模板 `.github/PULL_REQUEST_TEMPLATE.md`：复选清单（链接已验证 / 分类正确 / TL;DR ≤ 两句 / 非重复）。
- [ ] Issue 模板 `.github/ISSUE_TEMPLATE/`：新增条目建议、失效链接报告各一份。

## 4. 进主列表（sindresorhus/awesome）的要求与流程

硬性条件：

1. **仓库至少存在 30 天**（从首个实质 commit 起算）—— 新仓库立刻提 PR 会被直接关闭。
2. Topics 含 `awesome-list`、`awesome`；标题格式 `# Awesome-xxx` 且标题旁紧跟徽章。
3. 有 CONTRIBUTING.md 和 Code of Conduct；`npx awesome-lint` **零报错**。
4. "curation, not collection"：每条目有说明性描述，只收真正 awesome 的内容。
5. 先搜主列表确认没有同主题列表，避免重复。

⚠️ **格式取舍（重要）**：主列表明确要求 `- [Title](url) - Description.` 纯列表格式、**拒绝表格**。两条路线：

- **(a) 学术表格风**（Awesome-Loop-Models 风格：日期 + TL;DR + 表格）：对读者更友好，很多高星学术 awesome 仓库（如 Awesome-Diffusion-LLM）都如此，但不追求进主列表。
- **(b) 标准列表风**：可进主列表，获得官方流量入口。

建议：先以学术可用性优先积累内容，仓库成熟后再评估是否改格式提 PR。提交时 PR 只添加**一个条目**（你的列表）到主列表对应分类下。

## 5. 运营与增长

- [ ] **News 板块**：倒序、每条一行、含日期（如 `2026-07: added 6 RL-for-dLLM papers`）；超过 10 条折叠。更新频率是学术列表的核心竞争力——每周/每月固定更新比一次性塞 200 篇更能积累 star。
- [ ] **条目标签**：表格中用 emoji 或 shields 小徽章标注 `🤗 HF` / `💻 Code` / `📊 Bench` / Venue。
- [ ] **常见雷区**：不用 URL 短链；不收自己没读过的论文；arXiv 统一 `arxiv.org/abs/xxxx.xxxxx`；失效仓库标 `[Archived]` 而非删除。

## 6. 可选增强

- [ ] **GitHub Pages 交互浏览器**：轻量用 docsify（零构建直接渲染 README）或 Jekyll；进阶可用脚本把 README 解析成 `papers.json` + 静态前端（List.js 或 React+Vite 构建到 `gh-pages`）实现按分类/venue/年份过滤与搜索。参考 awesome.ecosyste.ms。
- [ ] **自动化**：GitHub Action 每日抓 arXiv `cs.CL` 关键词（"diffusion language model"）新论文并开 Issue 提醒；用 GitHub API 定期刷新各仓库 star 徽章。
- [ ] **Star History**：README 底部嵌入 star-history.com 图表。

## 7. 上线前最终检查

- [ ] `npx awesome-lint` 零报错（若走主列表路线）
- [ ] 所有链接可访问（lychee 通过）
- [ ] News / Contents / License / Contributing 四个板块齐全
- [ ] Topics、徽章、CC0 LICENSE、CoC 就位
- [ ] research_summary.md 中的 [待核实] 条目已逐条复核完毕
