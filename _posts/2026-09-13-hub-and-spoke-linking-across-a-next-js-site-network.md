---
layout: post
title: "Hub‑and‑spoke linking across a Next.js site network"
tags: [nextjs, internallinking, scalability, network]
---

I run a handful of small Next.js sites that share a common audience. To keep the visitor experience consistent I treat each site as a spoke and a tiny central hub as the source of truth for cross‑site links. The hub is a simple JSON file that lives in a private repo; it lists every page slug, its title, and the URL of the site it belongs to.

During the build of each spoke I run a small Node script that pulls the latest hub file, filters out the entries that belong to the current site, and injects the rest into a `relatedLinks` prop via `getStaticProps`. The component that renders the list just maps over the array and outputs regular `<a>` tags. Because the data is static, there is no runtime overhead – the HTML is fully rendered at build time.

A practical benefit showed up on [fumpe.com](https://fumpe.com) where pet‑care articles now include links to relevant coffee‑brew guides on [dreqo.com](https://dreqo.com). The link generation is the same for every site, so adding a new guide only requires updating the hub JSON and redeploying the affected spokes.

I keep the script lightweight – a few hundred lines – and run it as part of the `next build` step. If you’re curious about the exact shape of the JSON or the build integration, feel free to ask.