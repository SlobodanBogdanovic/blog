---
title: "API Response Simulator"
date: 2026-11-28
layout: post
categories:
  - Development
tags:
  - Chrome
  - API
  - Frontend
  - Testing
excerpt: "API Response Simulator intercepts fetch and XMLHttpRequest in the browser and returns a fake response without calling the real server."
---

Intercept HTTP requests (`fetch` and `XMLHttpRequest`) in the browser and return fake responses — without the real server ever being called. Built for front-end developers who need to mock APIs during development, testing, or demos.

## Download and install

The built extension is the [`dist` folder on `main`](https://github.com/SlobodanBogdanovic/APIResponseSimulator/tree/main/dist). You do not need Node.js or npm.

1. Download the repository: [APIResponseSimulator-main.zip](https://github.com/SlobodanBogdanovic/APIResponseSimulator/archive/refs/heads/main.zip)
2. Unzip it and open the `dist` folder inside (`APIResponseSimulator-main/dist`)
3. Open Chrome and go to `chrome://extensions`
4. Enable **Developer mode** (toggle in the top-right corner)
5. Click **Load unpacked**
6. Select that **`dist`** folder

Direct folder: https://github.com/SlobodanBogdanovic/APIResponseSimulator/tree/main/dist

After a later download, click the **refresh icon** on the extension card in `chrome://extensions` so Chrome picks up the updated `dist`.

## What it does

- Intercepts `fetch` and `XMLHttpRequest` requests matching your rules
- Returns your configured status code and response body
- Works on any page including `localhost`
- Rules are toggled on/off instantly — no page refresh needed
- Zero network traffic for intercepted requests (they never leave the browser)

Only `fetch` and `XMLHttpRequest` calls made by page JavaScript are intercepted. Requests from other extensions, the browser itself, native apps, or service workers inside the page are not. Rules are stored in this browser profile via `chrome.storage.local`. They apply to every tab while the extension is enabled.

## Quick start

### 1. Pin the extension

After loading, click the puzzle icon in Chrome's toolbar and pin **API Response Simulator**.

### 2. Open Settings

Click the extension icon, then click **Open settings**.

![Options page with no rules](https://github.com/user-attachments/assets/c2eb3de5-6dce-4870-a0e9-795e6250c0a0)

### 3. Add a rule

Click **Add rule** and fill in the form:

| Field | Example | Notes |
|---|---|---|
| Name | `List users` | A label for yourself |
| URL pattern | `localhost:3000/api/v1/users` | Host and port are an example. See pattern syntax below. |
| Method | `GET` | Or `ANY` to match all methods |
| Status code | `200` | Any HTTP status 100–599 |
| Response body | `[{"id": 1, "name": "Ada"}]` | Any text or JSON string |
| Response headers | `x-debug: true` | `Content-Type: application/json` is always included |
| Delay ms | `0` | Add artificial latency if needed |

Click **Save rule**.

![Options page with the List users rule turned on](https://github.com/user-attachments/assets/6105bc4f-0148-4c58-bed3-f88c1c59c8fd)

### 4. Refresh your app tab

Go to your application page and refresh it. Matching requests will now be intercepted.

The toolbar popup uses the same switches. The header toggle turns interception on or off for every rule. Each rule has its own switch.

![Popup with the extension and the rule turned on](https://github.com/user-attachments/assets/81e5ffd1-c121-4532-a893-64f445730a25)

A page that calls `fetch('https://jsonplaceholder.typicode.com/users')` receives the rule body instead of the real API:

![Page showing the mocked users JSON](https://github.com/user-attachments/assets/13a04dea-44ef-49c1-9bce-2a3bc32db24a)

## URL pattern syntax

Patterns match against both the full URL and the protocol-stripped URL, so you can omit `http://`.

| Pattern | Matches |
|---|---|
| `localhost:8080/api/v1/users` | Exact URL, any protocol |
| `localhost:8080/api/*` | Any path under `/api/` |
| `localhost:8080/api/v*/users` | `/api/v1/users`, `/api/v2/users`, and so on |
| `*/api/users` | Any host, path `/api/users` |
| `localhost:8080/*` | All requests to localhost:8080 |

- `*` matches any sequence of characters (including `/`)
- `?` matches any single character
- Matching is case-insensitive
- Protocol (`http://` / `https://`) is optional in the pattern

## Managing rules

**Enable or disable one rule.** Toggle the switch on the rule card in Settings, or use the per-rule toggle in the popup.

**Enable or disable all interception.** Click the extension icon, then use the toggle in the header. When it is off, all requests pass through regardless of rules.

**Edit a rule.** Click **Edit** on the rule card. All fields can be changed. Click **Save rule**.

**Delete a rule.** Click **Delete** on the rule card, then **Confirm**. No browser dialogs are used.

**Import and export.** **Export** downloads the current rules as `api-response-simulator-rules-YYYY-MM-DD.json`. **Import** appends rules from a JSON file. Existing rules are not modified or removed.
