---
layout: page
title: "Playwright Test Runner"
permalink: /playwright/test-runner/
---

## Playwright Test Runner

Playwright comes with a **built-in test runner** that makes it easy to run, organize, and report your tests.  
You don’t need any extra test framework — everything is included.

---

## 1️⃣ Run All Tests

To run all tests in your project:

```bash
npx playwright test
````

* Tests are automatically discovered from files ending with `.spec.ts` or `.spec.js`
* Results are shown in the console

---

## 2️⃣ Run a Specific Test File

If you want to run only one test file:

```bash
npx playwright test example.spec.ts
```

* Saves time when debugging or working on a specific feature

---

## 3️⃣ Run a Specific Test by Name

You can run a test by its name using the `-g` flag:

```bash
npx playwright test -g "Open Google homepage"
```

* Useful if you have many tests but want to run just one

---

## 4️⃣ Run Tests in Headed Mode

By default, tests run in **headless mode** (browser UI hidden).
To see the browser:

```bash
npx playwright test --headed
```

* Helps you **watch tests run** and debug visually

---

## 5️⃣ Run Tests in Parallel

Playwright can run tests **in parallel** to save time:

```bash
npx playwright test --workers=3
```

* `--workers=N` → number of parallel browser instances
* Parallel execution is **default**, so tests run faster automatically

---

## 6️⃣ View HTML Test Reports

After running tests, generate a visual report:

```bash
npx playwright show-report
```

* Opens a browser with **test results, passed/failed tests, and screenshots**
* Makes debugging easier

---

## 7️⃣ Filter by Tag or Project (Advanced)

You can organize tests using **tags**:

```ts
// example.spec.ts
test.describe('Login Tests @smoke', () => {
  test('Valid login', async ({ page }) => { ... });
});
```

Run only tests with the `@smoke` tag:

```bash
npx playwright test --grep @smoke
```

---

## Example: Full Test Run

```bash
# Run all tests
npx playwright test

# Run a specific test
npx playwright test example.spec.ts

# Run a specific test by name
npx playwright test -g "Valid login"

# Run in headed mode
npx playwright test --headed

# Show HTML report
npx playwright show-report
```

---

## Why Playwright Test Runner Is Powerful

* **No extra setup** — built-in test framework
* **Parallel execution** — faster tests
* **Filtering and tagging** — run only relevant tests
* **HTML reports** — easy debugging
* **Cross-browser support** — run on Chromium, Firefox, WebKit

---

## Next Step

👉 [Page Object Model (POM)](/playwright/page-object-model/)

---

