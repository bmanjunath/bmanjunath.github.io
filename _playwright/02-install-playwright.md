---
layout: default
title: "Installing Playwright"
permalink: /playwright/02-install-playwright/
---

## Installing Playwright (Step-by-Step)

Playwright is easy to install and works on **Windows, Mac, and Linux**.  
Follow this guide to get started quickly.

---

## Prerequisites

Before installing Playwright, make sure you have:

- Node.js installed (version 18 or later)
- A code editor (VS Code recommended)

Check Node.js version:

```bash
node -v
````

---

## Step 1: Create a Project Folder

Create a folder for your project and navigate into it:

```bash
mkdir playwright-demo
cd playwright-demo
```

---

## Step 2: Initialize a Playwright Project

Run the following command to initialize Playwright:

```bash
npm init playwright@latest
```

During installation, you will be prompted to:

* Choose **TypeScript** or **JavaScript**
* Select **Playwright Test Runner**
* Allow Playwright to install browsers → **Yes**

---

## Step 3: Verify Installation

Run your first test to make sure everything is working:

```bash
npx playwright test
```

If the test passes ✅, Playwright is installed correctly.

---

## What Gets Installed?

After initialization, you will have:

* Playwright Test Runner
* Chromium, Firefox, WebKit browsers
* Example tests
* Playwright configuration file

---

## Next Step

👉 [Your First Playwright Test](/playwright/first-test/)

---

