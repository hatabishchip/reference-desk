---
layout: post
title: "Using GSC to Choose Topics for My Content Network"
tags: [seo, content, gsc, network]
---

I've been running a small network of content sites for the past two years. The biggest lesson I've learned is that guessing topics rarely pays off. Instead I let Google Search Console (GSC) tell me what people are already looking for.

Every month I export the performance report for each property and pull the query list with impressions over 500 and average position better than 25. I drop any queries that have a click-through rate below 2 % because they usually indicate mismatched intent. The remaining list is sorted by impression count, and I pick the top 10-15 that fit the editorial focus of the site.

For a finance guide site like [qepam.com](https://qepam.com) I end up with queries such as "how to budget with a variable income" or "best high-interest savings account for students". Those are exact phrases people type, so the headline and sub-headings can mirror the query without sounding forced.

On the AI-tools awards blog [aceju.com](https://aceju.com) the process is the same, but I also filter for "weekly" or "best" because the editorial calendar is time-boxed. After the list is set, I create a simple spreadsheet that maps each query to a target URL, a primary keyword, and a brief outline. The page is then built in a markdown-first workflow, published, and I monitor the GSC data the following week to see if impressions move.

The whole pipeline is a few shell scripts and a small Python helper that normalises the CSV export. It isn’t fancy, but it removes a lot of the guesswork.

Happy to answer any questions about the GSC pipeline if you’re curious.