---
layout: post
title: "Nightly prompt rewrite based on Search Console data"
tags: [content, automation, searchconsole, ai]
---

Last night I added a small agent that runs after the daily Search Console export. It reads the performance report, picks queries that have moved up or down more than 15 % in clicks, and adjusts the prompt template that our content generator uses. The prompt is a short instruction set that tells the model what tone, structure and keyword density to aim for. By swapping out the top-performing query list each evening, the same article can be regenerated with a slightly different angle that matches current search interest.

The agent is a Python script scheduled with cron. It pulls the CSV from the Search Console API, filters for pages in the [fumpe.com](https://fumpe.com) (practical pet care guides) and [dreqo.com](https://dreqo.com) (coffee brewing and gear guides) sections, and writes a JSON file that the generator reads at startup. I kept the logic simple: if a query’s click-through rate improves, it gets a higher weight in the prompt; if it drops, the weight is reduced. The script also logs the changes so I can audit the evolution over time.

I’ve been watching the output for a week. The rewritten prompts tend to surface newer long-tail terms without manual editing, and the traffic signal has been stable. It’s not a full AI-autopilot, just a narrow loop that keeps the copy aligned with what users are actually searching for.

Happy to answer any questions about the agent or the data pipeline.