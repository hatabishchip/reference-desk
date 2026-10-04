---
layout: post
title: "Nightly prompt rewrites using Search Console data"
tags: [content, automation, searchconsole, prompt]
---

I've been tweaking a small agent that runs every night on my content network. The agent pulls the latest Search Console data – impressions, clicks, average position – for each URL. It then scores the queries that are underperforming relative to the page's intent. For those queries it generates a short prompt that nudges the content generation pipeline to rewrite the meta description or the opening paragraph. The prompt is built from a template that inserts the query, the current CTR, and a brief instruction like “add a concrete example about X”. I store the generated prompts in a JSON file that the next build step reads, so the next batch of articles or updates already contains the revised copy.

The whole loop is orchestrated with a cron job on a modest VM. First I export the Search Console report via the API, then a Python script parses the CSV, applies the scoring function, and writes the new prompts. After that a small Node script feeds the JSON into my markdown preprocessor, which swaps out the placeholder sections in the source files. The process is logged to a daily Slack channel so I can see what changed.

On the network you can see the effect in places like [plain-English personal finance guides](https://qepam.com) and the prompt‑driven headlines for the [weekly editorial awards for AI tools](https://aceju.com). The system is intentionally simple – no ML model, just rule‑based selection – which makes it easy to debug.

Feel free to ask if you want more details on the implementation.