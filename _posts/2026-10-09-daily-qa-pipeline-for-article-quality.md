---
layout: post
title: "Daily QA Pipeline for Article Quality"
tags: [contentgen, qa, ai, pipelines]
---

Hey everyone,

I wanted to share a bit about a technical piece of the content network I'm building, specifically the daily QA pipeline. When you're running sites like [gotfo.com](https://gotfo.com), which focuses on home gardening how-tos, or [afixu.com](https://afixu.com), covering home improvement and DIY tool guides, maintaining a consistent quality bar across thousands of articles becomes a challenge.

My solution is a daily automated pipeline. It pulls every article published or updated in the last 24 hours, then runs it through a series of checks. The core of it involves scoring each piece on a few dimensions: depth of information, structural integrity (heading hierarchy, readability), and what I call 'anti-AI patterns'. The anti-AI part isn't about detecting AI as much as it is about identifying characteristics that make content feel generic or unhelpful, things like repetitive phrasing, lack of specific examples, or overly simplistic explanations where detail is needed.

Articles that fall below a certain threshold on any of these scores are flagged. The pipeline then sends them back through an auto-regeneration process, which uses a combination of custom prompts and contextual data from the article's topic to rewrite or expand specific sections. It's not perfect, but it dramatically reduces the number of articles that need manual review and helps push everything towards a higher baseline quality.

It's been a useful way to scale content while trying to keep it genuinely helpful and distinct. Happy to answer any questions about the technical implementation of this pipeline.