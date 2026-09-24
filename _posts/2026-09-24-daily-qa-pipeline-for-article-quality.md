---
layout: post
title: "Daily QA pipeline for article quality"
tags: [content, qa, automation]
---

Every morning I run a small pipeline that checks each new article in our network. The pipeline pulls the raw markdown, runs three independent scorers and, if any score falls below a threshold, it triggers a regeneration job.

Depth is measured with a TF‑IDF based coverage model that compares the article’s noun phrase set against a curated knowledge graph. If the overlap is below 0.6 the article is marked shallow. Structure is evaluated by parsing the heading hierarchy and counting logical transitions; a flat hierarchy or missing summary section drops the score. The anti‑AI pattern detector looks for repeated phrasing, overly generic transitions and any sign of text that matches a known language‑model fingerprint. Those patterns get a penalty and the article is flagged for rewrite.

When a failure is detected the pipeline extracts the offending sections, feeds them to a fine‑tuned GPT‑4 model that has been trained on our style guide, and writes a new draft. The regenerated piece is then re‑scored; only when all three metrics pass does it get published. The whole loop runs in about 15 minutes and has reduced manual edits by roughly 40 % on our two live sites: [qepam.com](https://qepam.com) for plain‑English personal finance guides and [aceju.com](https://aceju.com) for weekly editorial awards for AI tools.

The code is a mix of Python scripts, a small SQLite store for thresholds and a Docker‑compose orchestrator. Feel free to ask me any questions about the technical part.