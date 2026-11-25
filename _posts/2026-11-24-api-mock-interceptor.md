---
title: "Response Simulator: mock an API in the browser"
date: 2026-11-24
layout: post
categories:
  - Development
tags:
  - Chrome
  - API
  - Frontend
  - Testing
excerpt: "Frontend work often waits on an API that is unfinished, unstable, or owned by another team."
---

Frontend work often waits on an API that is unfinished, unstable, or owned by another team. A demo can fail for the same reason: the screen is ready, and the response it needs is not. Waiting, hard-coding a mock inside the app, or skipping the scenario each costs time or leaves a behavior untested.

[**APIResponseSimulator**](https://github.com/SlobodanBogdanovic/APIResponseSimulator) is a Chrome extension for that gap. It sits beside the page and answers the calls you choose, so the UI can be built and shown against a response you control. The application stays as it is. It receives a normal HTTP response and keeps going.

A rule is a small contract: HTTP method, path pattern, status code, and response body. When the page sends a request that matches the method and the path, the extension returns that status and body. That call stays in the browser. The real server is left out of it. Requests that match no rule continue to the API they were written for.

The practical cases are the ones a shared backend is bad at providing on demand. An empty list, a validation error, a 401, or a 500 can be returned for one screen, so the empty state, the error state, and the happy path can all be exercised on the real page. A demo can use the same rules and stay stable when the shared environment is down or still changing.

The loop stays short. Install the extension, add the rules for the screen you are on, refresh the tab, and continue. There is no mock server to run and no mock module to check into the repository. Rules are stored in the browser, so they are still there the next time you open Chrome. Each browser keeps its own copy. When someone else needs the same behavior, they add the same rules on their machine.

It covers the HTTP traffic a web app sends from the browser while you develop or demo.

I am still working on the extension. I will publish it on the Chrome Web Store soon.

---

*Source: [APIResponseSimulator](https://github.com/SlobodanBogdanovic/APIResponseSimulator).*
