---
title: New website
description: I created a new website for me with Deno, Lume and GitHub Pages.
date: 2023-10-15T12:00
tags:
  - coding
order: 1
---

11 years ago, I was an aspiring musician that needed a website. I went to Google and found a step-by-step guide for creating a WordPress site. The guide was apparently written by an Australian person because it recommended a hosting provider that was based in Australia. I bought the hosting plan and registered joonasnuutinen.com as my domain.

I remember sitting for hours at my computer, browsing themes, tweaking fonts and colours and coming up with content. Sometimes I needed more than my selected theme provided and ended up blindly copy-pasting some CSS snippets I had found online with zero understanding of what it does. Sometimes I needed something even more powerful, had to create a child theme and insert some random-looking lines of PHP to my functions.php. I started getting glimpses of the vast world of web development and it felt both overwhelming and intriguing at the same time.

I went through many iterations with my WordPress site. One of the first issues I had was the slowness. It occurred to me that getting a hosting plan from an Australian company was probably not the wisest decision for someone based in Finland. I switched to a Finnish provider and had to figure out how to move files with FTP, transfer a domain and so on.

At some point I decided to buy a commercial theme called [X](https://themeforest.net/item/x-the-theme/5871901). It had a proprietary page builder built on top of the WordPress core. I could create all kinds of cool stuff with the bloated CSS and JavaScript libraries that were included.

Then later I learned to create my own themes from [Underscores](https://underscores.me/). I wanted to ditch the paid theme and create one of my own. At this point I realised that X's page builder was actually a vendor lock-in and there was no easy way to migrate the content back to core WordPress.

Then came Gutenberg and I switched to that. Then came the Site Editor and it was again time to update. By this point I was already a professional web developer and had aspirations to move away from WordPress to something more technical.

I had learned to appreciate simplicity. I wanted to avoid unnecessary bloat and just have a really minimalistic website, preferrably with static site generation. I had worked with Next.js but React felt like an overkill for my simple purposes. I tried Hugo but was too busy (or lazy) to learn Go.

I had stumbled across [Deno](https://deno.com/) a couple of times and found out that there's an SSG framework called [Lume](https://lume.land/) for Deno. I gave it a spin and really liked it. It had everything I needed, was easy to learn, provided a nice developer experience (hot reloading ❤️) and had Markdown support and file-based routing out of the box.

So, now I have a new website again. 11 years with WordPress was a long relationship and had its ups and downs. In the end, it was just too much for me. Paying for a LAMP server and having a no-code admin dashboard with plugins and updates and everything started to feel like a burden. Now everything is [under one GitHub repository](https://github.com/joonasnuutinen/joonasnuutinen.github.io) that builds and deploys the static site to GitHub Pages whenever I push and update to main. No servers and databases to manage, just me, my code editor and a bunch of Markdown files. This feels good (for now).