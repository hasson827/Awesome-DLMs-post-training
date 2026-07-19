# Contributing Guidelines

Thank you for your interest in **Awesome-DLMs-post-training**! This repository is a carefully curated (curation, not collection) list of papers and resources on **post-training for Diffusion Language Models (DLMs)**. We welcome contributors from all backgrounds — issues and PRs may be written in either English or Chinese.

## Scope

✅ **In scope** — for masked/absorbing diffusion LMs, continuous diffusion LMs, and multimodal diffusion LMs:

- Alignment & post-training: SFT / instruction tuning / RLHF / DPO / KTO / GRPO-style RL post-training / RLVR
- Reasoning: reasoning / CoT / planning-oriented post-training
- Distillation & efficiency: step distillation, few-step sampling training, classifier-free guidance training, speculative decoding, confidence-aware fine-tuning
- Adaptation techniques: AR→DLM conversion fine-tuning, long-context post-training
- Evaluation benchmarks, open-source training frameworks, and surveys

❌ **Out of scope**:

- Pure pre-training architecture papers (unless they include a clear post-training component)
- Autoregressive LM papers (methods on AR LLMs, e.g. "diffusion-inspired" work like DART, require an explicit justification of relevance to DLMs)
- DPO/GRPO for image/video diffusion models (e.g. Diffusion-DPO, D3PO, BranchGRPO), unless directly applicable to text DLMs
- Papers you have not read yourself — please make sure you understand the content of any entry you submit

## Entry Format

One entry per paper, placed under the appropriate category section, **sorted by date in descending order** (newest first). Format:

```markdown
- [MM/DD/YYYY] **Paper Title**
  - **Authors:** First Author, Second Author, … (affiliation optional) · Venue (e.g. NeurIPS 2025 / arXiv 2025)
  - **TL;DR:** One or two sentences summarizing the core contribution.
  - [arXiv](https://arxiv.org/abs/xxxx.xxxxx) · [GitHub](https://github.com/org/repo) (if official code exists)
```

Requirements:

- arXiv links must use the `https://arxiv.org/abs/xxxx.xxxxx` format — no short links, no version suffixes.
- The TL;DR should be one or two sentences highlighting "what was done + why it matters"; do not copy the abstract verbatim.
- GitHub links should point only to **official or author-endorsed** repositories; verify the link is reachable (HTTP 200) before submitting.
- Mark any information you could not confirm with `[TODO: verify]` (e.g. author lists, venues, repository links) — never guess or fabricate.
- Each paper appears exactly once, in its single most appropriate category; cross-cutting work may note the connection inside its primary entry.

## Submission Process

1. Fork this repository and create a new branch (e.g. `add-diffugrpo-paper`).
2. **One PR does one thing** (add one paper / fix one class of links / update one category).
3. PR title format: `Add <paper short name>`, e.g. `Add TraDo (TraceRL)`.
4. In the PR description, check off and fill in the template checklist:
   - [ ] I have verified that the arXiv / GitHub links are reachable
   - [ ] The entry is in the correct category and inserted in reverse chronological order
   - [ ] The TL;DR is no more than two sentences
   - [ ] I have confirmed this is not a duplicate (please search the existing list first)
5. If CI is configured for the repository (awesome-lint / link checking), make sure all checks pass before requesting review.

## Metadata Conventions

- **Venue**: prefer the formally published venue (NeurIPS 2025, ICLR 2026, etc.); use `arXiv 2025` for unpublished work; mark uncertain venues with `[TODO: verify]`.
- **Date**: use the arXiv v1 submission date in MM/DD/YYYY format; if only the month can be confirmed, use MM/YYYY.
- **Optional badges**: small badges after an entry are encouraged to mark resources, e.g. `🤗 HF` (Hugging Face weights), `💻 Code`, `📊 Bench`.
- **Dead repositories**: when an official repository is archived or deleted, do not remove the entry — mark it `[Archived]` with a note.

## Reporting Issues

- Found a dead link, incorrect metadata (authors, venue, date), or a mis-categorized entry: open an issue with a `[Fix]` / `[Link]` title prefix.
- Want to suggest a whole new category or a batch of papers: open an issue with a `[Suggest]` title prefix and discuss before submitting a large PR.

## Code of Conduct

By participating in this project, you agree to abide by the [Contributor Covenant v2.1](https://www.contributor-covenant.org/version/2/1/code_of_conduct/) Code of Conduct. Please be kind and professional.

Thank you again for your contribution! 🎉
