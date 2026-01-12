---
layout: page
title: "Installing Playwright"
permalink: /playwright/install-playwright/
---

## Installing Playwright (Step-by-Step)

Playwright is easy to install and works on **Windows, Mac, and Linux**.

---

## Prerequisites

Before installing Playwright, make sure you have:

- Node.js installed (version 18 or later)
- A code editor (VS Code recommended)

👉 Check Node.js:
```bash
node -v


Ah! Now I understand perfectly — thank you for clarifying. 😅

No — you **cannot copy instructions like “create project folder” or “during installation you will be asked…”** as code into a Markdown code block and expect it to run. Those are **instructions**, not commands. Only **actual shell commands** go inside code blocks.

So a correct `.md` file for **Installing Playwright** should be structured like this:

---

**File:** `playwright/install-playwright.md`

````markdown
---
layout: page
title: "Installing Playwright"
permalink: /playwright/install-playwright/
---

# Installing Playwright

Playwright works on **Windows, Mac, and Linux**.

## Prerequisites

Make sure you have:

- Node.js installed (version 18 or later)
- A code editor (VS Code recommended)

Check Node.js version:

```bash
node -v
````

## Install Playwright

1. Create a project folder and navigate into it:

```bash
mkdir playwright-demo
cd playwright-demo
```

2. Initialize a new Playwright project:

```bash
npm init playwright@latest
```

> During installation, you will be prompted to:
>
> * Choose **TypeScript** or **JavaScript**
> * Select **Playwright Test Runner**
> * Allow Playwright to install browsers → **Yes**

3. Verify installation by running a test:

```bash
npx playwright test
```

If the test passes, Playwright is installed correctly.

## What got installed?

* Playwright Test Runner
* Chromium, Firefox, WebKit browsers
* Example tests
* Playwright config file

```

---

