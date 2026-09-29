---
layout: post
title: "Hub-and-spoke internal linking for a Next.js site network"
tags: [nextjs, seo, linking, scaling]
---

I've been running a small network of Next.js sites that each focus on a narrow topic – for example, a home gardening how-to site at [gotfo.com](https://gotfo.com) and a DIY tool guide at [afixu.com](https://afixu.com). To make the whole collection feel like a single resource for search engines and readers, I set up a hub-and-spoke internal linking model.

The hub is a lightweight index page that lives in a dedicated repo. It contains a JSON manifest of all spokes, their primary keywords and the URLs of their most important articles. During the build of each spoke I import that manifest with a simple fetch in getStaticProps. The page then renders a list of related articles from the other spokes using next/link, which gives me pre-fetching and client-side navigation for free.

Because the manifest is version-controlled, any change to a spoke – a new article, a renamed slug – is propagated to the hub and all other spokes the next time they rebuild. I use incremental static regeneration with a revalidate interval of 300 seconds, so the sites stay fresh without a full redeploy.

The only tricky part was avoiding circular dependencies. I keep the manifest read-only in the hub and treat the spokes as consumers only. A tiny node script runs after each successful build to push the updated manifest back to the hub repo, then triggers a Vercel webhook for the other sites.

If you’re curious about the fetch-and-render pattern or the webhook setup, let me know.