---
layout: post
title: "GSC-driven topic selection for my content sites"
tags: [content, seo, gsc, network]
---

I run a small network of niche content sites. Over the past year I let Google Search Console (GSC) drive the editorial calendar instead of brainstorming titles.

Each month I export the "Performance" report for the whole property, filter for queries with impressions above 200 and average position better than 12. I then sort by clicks and drop any terms that already have a dedicated article. The remaining list becomes the backlog. Because the data is already filtered by real search volume, the risk of publishing something nobody looks for drops dramatically. I also keep an eye on the "Pages" tab to see which existing posts are gaining traction; a small tweak to the headline or a deeper sub-topic often yields a quick bump.

For instance the pet-care guide at [fumpe.com](https://fumpe.com) grew from a handful of clicks to several hundred after I added a section on "how often to trim a dog's nails" - a query that showed up in the GSC export but wasn't covered before.

Similarly the coffee-gear roundup on [dreqo.com](https://dreqo.com) was expanded with a page on "budget burr grinder maintenance" after the term appeared with 150 impressions and a 9.8 average position.

Automation: I run a simple Python script that hits the Search Console API, writes the filtered queries to a CSV, and pushes the file to a shared Google Sheet. The sheet is the single source of truth for the writers; they pick a query, draft an outline, and tag the row as "in progress".

A couple of gotchas: the API caps at 5,000 rows per request, so I paginate by date; and the "clicks" metric can be noisy for brand terms, so I add a manual exclusion list.

That’s the whole pipeline in a nutshell. Let me know if you want the script or more details on the filtering logic.