---
layout: page
title: "Your First Playwright Test"
permalink: /playwright/03-first-test/
---

## Your First Playwright Test

Now that Playwright is installed, let's write your **first automated test**.

This example will open a website and check its title.

---

## Step 1: Create a Test File

Create a file called `example.spec.ts` (or `.js` if using JavaScript):

```bash
touch example.spec.ts

```
## Step 2: Write a Simple Test
Open the file and add the following code:
```
ts

import { test, expect } from '@playwright/test';

test('Open Google homepage', async ({ page }) => {
  // Navigate to Google
  await page.goto('https://www.google.com');

  // Verify the page title
  await expect(page).toHaveTitle('Google');
});

```
## Step 3: Understand the Test

```
test('test name', async ({ page }) => {}) → defines a test case

page.goto(url) → opens a website

expect(page).toHaveTitle('title') → verifies the page title

```

Playwright automatically waits for the page to load before checking the title.

## Step 4: Run the Test
In your project folder, run:
```
bash

npx playwright test
You should see output like:
```
sql
```
Running 1 test using 1 worker
✓ example.spec.ts: Open Google homepage
1 passed
✅ Congratulations! Your first Playwright test passed.
```

## Step 5: Run Test in Headed Mode
To see the browser while the test runs:
```
bash

npx playwright test --headed
```
This is helpful for learning and debugging.


### Why This Test Is Powerful
No WebDriver setup required
Works on Chromium, Firefox, and WebKit
Auto-waits make tests less flaky
Can scale to multiple pages, actions, and assertions

---

## Next Step

👉 [Locators & Selectors](/playwright/locators)

---
