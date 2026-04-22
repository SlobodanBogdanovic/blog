---
title: "NinjaInterceptor"
date: 2026-04-22
layout: post
categories:
  - Development
tags:
  - Chrome
  - API
  - Frontend
  - Testing
excerpt: "When you are testing against an API that is not ready, unstable, or owned by someone else, the usual options are not good."
---

When you are testing against an API that is not ready, unstable, or owned by someone else, the usual options are: wait for the backend team, mock responses inside your codebase, or skip the scenario entirely. None of these are good.

**NinjaInterceptor** is a Chrome extension that works alongside your app in the browser. You define rules—method, path pattern, status, and body—and matching requests from your page are answered with what you configured. The real server is not involved for those calls. Your application does not need to change; it simply sees a normal response.

It is aimed at frontend work: the HTTP traffic your web app issues while you develop or demo. It is not a whole-machine proxy, so things like CLI clients or services running outside the browser are out of scope. Your rules are stored with the browser, so they are still there after you close Chrome. If the team wants the same behavior, you line up the same rules in each browser—nothing syncs automatically.

Nothing runs as a separate backend: no daemon, no checked-in mock layer, no extra service to babysit. Install the extension, add rules, refresh the tab, and go.

---

*The repository is currently private. If you want access, send me a message and I will add you.*
