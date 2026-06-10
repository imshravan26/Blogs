---
title: "Rendering Patterns in Modern Web Development"
seoTitle: "SSR, CSR, SSG, ISR, Hydration and Islands Explained"
seoDescription: "SR, SSR, SSG, ISR, Hydration, and Islands Architecture. What they are, how they work, and when to actually use each one."
datePublished: 2026-05-28T20:41:08.662Z
cuid: cmppyk4dt002s1sqk50in3f1r
slug: rendering-patterns-in-modern-web-development
cover: https://cdn.hashnode.com/uploads/covers/6836cc7a1c8efb431960e9f0/33be305e-bad5-4631-9dcb-e0a6611418a6.png
tags: javascript, performance, web-development, architecture, reactjs, client-side-rendering, ssr, server-side-rendering, nextjs, static-site-generation, astro, isr, csr, hydration, israel, islands, rendering-patterns, incremental-static-regeneration

---

## What are rendering patterns?

Every time you visit a webpage, your browser needs HTML to display it. Rendering is just the process of producing that HTML.

Now, rendering patterns are basically the different strategies for *how* and *where* that HTML gets produced. Do you build it on the server? In the browser? Ahead of time during a build step? Each of these is a different pattern, and each one has a different set of tradeoffs.

Lets dive deep in each design pattern..

## CSR : Client Side Rendering

In CSR, the server sends almost nothing. Just a bare HTML file with an empty `<div>` and a `<script>` tag pointing to your JavaScript bundle. The browser downloads that, runs the JavaScript, and *then* builds the page, right there in the browser.

So the server's job is basically just to hand over the JS files. The browser does all the actual rendering work.

![](https://cdn.hashnode.com/uploads/covers/6836cc7a1c8efb431960e9f0/4a86a1b1-6fe8-40a7-a223-8e13de8f0ef4.png align="center")

Think of it like a flat-pack furniture delivery. The server ships you the parts and the instruction manual. You assemble it yourself. The server didn't build you a chair, it gave you everything needed to build one.

The problem shows up on slow connections or low-end devices. The user is looking at a blank screen while the JS downloads, parses, and executes. That gap between "page requested" and "something actually appears" is wide in CSR.

SEO is the other issue. Search crawlers historically don't wait for JavaScript to run. They see your empty HTML shell and index nothing useful.

**Where you see it:** Internal tools, admin dashboards, anything sitting behind a login. Figma, Notion and other highly interactive apps where the content is different per user and SEO doesn't matter.

**Skip it when:** You're building anything public-facing. A marketing page, a blog, a product listing.

*CSR will hurt your load times and your search rankings.*

## SSR: Server-Side Rendering

SSR flips the model completely. Every time someone requests a page, the server generates the full HTML . It fetches the data, builds the markup, and ships a complete document to the browser.

The browser gets real, readable HTML on the very first response. No waiting for JavaScript. The page renders immediately.

![](https://cdn.hashnode.com/uploads/covers/6836cc7a1c8efb431960e9f0/a7fe845f-cd22-4e53-86ed-973f3726dff5.png align="center")

This is actually how the web worked before JavaScript frameworks took over. PHP, Rails, Django, all of these are SSR by default. You request a page, the server builds it, you get HTML back. Modern SSR is just that same idea applied to React and Vue running on a Node server.

Think of it like ordering food at a restaurant versus cooking at home. CSR is cooking at home, the ingredients arrive and you make the meal yourself. SSR is the restaurant doing everything, by the time it reaches you, it's ready to eat.

The tradeoff is **server compute**. Every single page load triggers a fresh cycle, hit the database, build the HTML, send the response. Under high traffic, that adds up fast. You also can't cache SSR responses the way you cache a static file, because the content might be different per user or per request.

**Where you see it:** E-commerce product pages where price and stock need to be real-time, news articles, social feeds, basically anything where the data changes constantly and needs to be accurate at the exact moment someone requests it.

**Skip it when:** Your content doesn't change much. Re-rendering the same HTML on every request is wasted compute if the output is identical every time.

## SSG : Static Site Generation

SSG takes the question of *when* to render and pushes it all the way back to before any user even visits. You run a build step, the framework fetches all the data it needs, generates every page as a plain HTML file, and you deploy those files to a CDN.

When someone visits, they're getting a pre-built file served from a CDN edge server closest to them. No database query. No server render. No waiting. Just a file.

![](https://cdn.hashnode.com/uploads/covers/6836cc7a1c8efb431960e9f0/14d72823-db5a-476a-9cc7-1054cb92f624.png align="center")

This is as fast as it gets. The HTML already exists before the request even happens. CDNs are globally distributed so the file is always close to whoever is asking for it.

Think of it like a book. The author wrote it once, it got printed thousands of times, and now anyone can pick up a copy instantly. Nobody is writing the book fresh every time someone wants to read it.

SEO is perfect because the HTML is fully formed and ready for crawlers. Performance is as good as it can be because there's no server in the critical path at all.

The limitation is obvious once you think about it, the content is frozen at build time. Your data is only as fresh as the last time you ran the build. If something changes, you need to rebuild and redeploy to see it reflected.

For a small blog that's fine. For a product catalog with fifty thousand items where prices change daily, rebuilding everything every few hours becomes a real problem.

**Where you see it:** Documentation sites, personal blogs, marketing landing pages, portfolio sites. The Tailwind docs, the Next.js docs, these are SSG. Content written by humans that doesn't change by the minute.

**Skip it when:** Your data updates frequently or you have too many pages for a build to be practical. A news site can't rebuild every five minutes.

## **ISR : Incremental Static Regeneration**

ISR is Next.js's answer to the stale data problem in SSG. The core idea is simple, you still get statically generated pages, but you give them an expiry time. After that window passes, the page gets rebuilt in the background.

You tell Next.js: *regenerate this page every 60 seconds*. After that interval, the next person who visits triggers a background rebuild. While that's happening, everyone still gets the cached version. Once the rebuild finishes, the fresh page takes over.

![](https://cdn.hashnode.com/uploads/covers/6836cc7a1c8efb431960e9f0/c2690caf-02df-4134-90d3-fceb761e38c6.png align="center")

The key thing to understand here is that ISR is stale-while-revalidate. The person who triggers the rebuild doesn't wait for it, they still get the old page. The *next* visitor after the rebuild completes gets the fresh one. That's a deliberate tradeoff to keep response times consistently fast.

Think of it like a notice board at an office. Someone updates it every morning. If you walk past at 2pm, the information might be from this morning, but not ancient either. Good enough for most things, and always instantly readable.

So you're getting the best of both worlds, the speed and cacheability of SSG, without the content going stale indefinitely. A 60 second revalidation window means your data is at most a minute behind at any point.

**Where you see it:** Product listing pages on e-commerce sites, blog index pages, sports score summaries, pages that need to be fast but can tolerate being slightly behind real-time.

**Skip it when:** You need truly real-time data. If you're showing live stock prices or a live cricket score, a 60 second old page is not good enough. That's a job for SSR.

## Hygration

Hydration is the mechanism that sits between SSR and interactivity, understanding it explains a frustrating experience almost everyone has had on the web.

Here's the problem. SSR gives you real HTML fast, which is great. But that HTML is completely inert. There are no event listeners attached. Buttons don't work. State doesn't exist. It's a photograph of a UI, not a live one.

Hydration is the process of JavaScript loading, running over that existing HTML, and waking it up. Attaching the React component tree to the DOM nodes that are already there, wiring up event listeners, initialising state.

![](https://cdn.hashnode.com/uploads/covers/6836cc7a1c8efb431960e9f0/7392da5e-45bc-4de4-8b5f-62318a08daa2.png align="center")

This is the source of something you've definitely encountered, a page that *looks* fully loaded but doesn't respond to clicks. That's the window between the HTML painting on screen and hydration completing. The UI is visible but the JavaScript hasn't finished waking it up yet.

That window matters more than people think. The browser still has to download the full JS bundle, parse it, and walk the entire component tree to hydrate it. On a large app this can take seconds. Your First Contentful Paint looks great because SSR got the HTML there fast, but Time to Interactive is still gated on hydration finishing.

**Where it shows up:** Any SSR or SSG app using a component framework. Next.js, Nuxt, Remix all of them do hydration. You don't configure it, it just happens.

## Islands Architecture

Islands is the idea that you shouldn't have to hydrate the entire page just because one part of it needs to be interactive.

Think about a typical blog post page. It's mostly text, maybe some images, a header, a footer. Completely static content that never changes. But somewhere on that page there's a search bar, a newsletter signup form, a like button. Those three things need JavaScript. Under standard SSR and hydration, you'd still ship and hydrate the entire React tree, every component on the page, just to make those three things work.

Islands says that's wasteful. Keep everything else as plain static HTML. Only hydrate the parts that actually need it.

![](https://cdn.hashnode.com/uploads/covers/6836cc7a1c8efb431960e9f0/38607644-8c67-4a2b-a382-0fe8293ad7d9.png align="center")

Each interactive component is an island. It hydrates independently, loads its own JavaScript, and doesn't wait for or block anything else on the page. The static content surrounding it never gets hydrated at all because it doesn't need to be.

Think of it like an actual archipelago. Each island exists on its own, surrounded by calm water. What happens on one island doesn't affect the others. The ocean between them just sits there, static and unbothered.

The result is dramatically less JavaScript shipped to the browser. Faster Time to Interactive. Better performance on low-end devices. The user gets the static content instantly and each interactive piece wakes up on its own without blocking the rest.

Astro is built entirely around this pattern. You write mostly static markup and opt specific components into interactivity using directives, `client:load` hydrates immediately, `client:visible` waits until the component scrolls into view. You only pay the JavaScript cost for the parts that genuinely need it.

**Where you see it:** Documentation sites with a search bar, blogs with a comment section, marketing pages with an interactive demo tucked somewhere in the middle.

**Skip it when:** Most of your UI is stateful and interactive. If every component needs JavaScript, there are no static stretches between your islands the pattern stops making sense.

#### So which one do you pick?

Every pattern we covered is solving the same problem from a different angle. The right one depends entirely on what you're building, what your data looks like, how interactive your UI needs to be, and what you can't afford to get wrong.

Here's a quick way to think about all of them together:

| Pattern | HTML is built | By whom | SEO | Interactivity | Best for |
| --- | --- | --- | --- | --- | --- |
| CSR | On every visit | Browser | Poor | High | Dashboards, logged-in apps |
| SSR | On every request | Server | Great | Medium | Dynamic, personalised pages |
| SSG | At build time | Build server | Great | Low | Blogs, docs, marketing sites |
| ISR | Build + revalidate | Build server | Great | Low | Frequently updated static pages |
| Islands | Build or request | Server + browser (selective) | Great | Selective | Content sites with interactive pockets |

A rough mental model for picking one:

*   Content doesn't change much → **SSG**
    
*   Content changes but can be slightly stale → **ISR**
    
*   Content needs to be fresh on every request → **SSR**
    
*   Content is all behind a login, SEO doesn't matter → **CSR**
    
*   Page is mostly static with a few interactive bits → **Islands**
    

Most modern apps don't pick just one. Next.js lets you use SSG, SSR, and ISR on different routes within the same project. A marketing page is SSG, a product page is ISR, a user dashboard is SSR or CSR. The patterns aren't mutually exclusive they're tools you reach for depending on what a specific page needs.