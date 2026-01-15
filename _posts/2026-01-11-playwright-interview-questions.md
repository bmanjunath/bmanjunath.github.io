---
layout: post
title: "Playwright Interview Questions & Answers (0–5+ Years)"
categories: [playwright, interview]
permalink: /post/playwright-interview-questions/
---

# 🎭 Playwright Interview Questions & Answers (with Code)

This guide covers **basic to advanced Playwright interview questions**, including **coding scenarios**, **framework design**, **debugging**, and **mock interviews**.

---

## 🟢 BASIC QUESTIONS (1–15)

### Q1. What is Playwright?
Playwright is an open-source end-to-end automation framework developed by Microsoft for testing web applications across Chromium, Firefox, and WebKit with a single API.

---

### Q2. Which browsers does Playwright support?
- Chromium (Chrome, Edge)
- Firefox
- WebKit (Safari engine)

---

### Q3. What languages does Playwright support?
- JavaScript / TypeScript
- Python
- Java
- C#

---

### Q4. What is auto-waiting in Playwright?
Playwright automatically waits for:
- Elements to be visible
- Enabled
- Stable
before performing actions.

```ts
await page.locator('#login').click();
````

---

### Q5. Difference between Playwright and Selenium?

| Playwright           | Selenium       |
| -------------------- | -------------- |
| Auto-waiting         | Manual waits   |
| Faster               | Slower         |
| Modern APIs          | Legacy APIs    |
| Built-in parallelism | External setup |

---

### Q6. What is `page` in Playwright?

`page` represents a single browser tab or window.

---

### Q7. What is `browserContext`?

An isolated browser session similar to an incognito window.

---

### Q8. What is headless mode?

Running tests without opening the browser UI.

```ts
npx playwright test --headless
```

---

### Q9. How do you launch headed mode?

```ts
npx playwright test --headed
```

---

### Q10. What are locators?

Locators provide a way to find elements with auto-retry support.

---

### Q11. Best locator strategy?

* `getByRole`
* `getByLabel`
* `getByTestId`

---

### Q12. What is `getByRole`?

Locates elements based on ARIA roles.

```ts
await page.getByRole('button', { name: 'Submit' }).click();
```

---

### Q13. What is strict mode?

Ensures only one element matches a locator.

---

### Q14. What is `expect` in Playwright?

Assertion library built into Playwright.

```ts
await expect(page).toHaveTitle('Dashboard');
```

---

### Q15. How do you install Playwright?

```bash
npm init playwright@latest
```

---

## 🟡 INTERMEDIATE QUESTIONS (16–35)

### Q16. How do you handle waits?

Avoid hard waits. Use auto-waiting or assertions.

```ts
await expect(locator).toBeVisible();
```

---

### Q17. How do you handle multiple tabs?

```ts
const [newPage] = await Promise.all([
  context.waitForEvent('page'),
  page.click('a[target=_blank]')
]);
```

---

### Q18. How do you handle alerts?

```ts
page.on('dialog', dialog => dialog.accept());
```

---

### Q19. How do you upload a file?

```ts
await page.setInputFiles('input[type=file]', 'test.pdf');
```

---

### Q20. How do you download a file?

```ts
const download = await page.waitForEvent('download');
await download.saveAs('file.pdf');
```

---

### Q21. How do you handle frames?

```ts
const frame = page.frame({ name: 'frameName' });
await frame?.click('#submit');
```

---

### Q22. How do you handle dropdowns?

```ts
await page.selectOption('#country', 'India');
```

---

### Q23. How do you retry failed tests?

```ts
retries: 2
```

---

### Q24. How do you group tests?

```ts
test.describe('Login Tests', () => {});
```

---

### Q25. How do you run a single test?

```bash
npx playwright test login.spec.ts
```

---

### Q26. What is test isolation?

Each test runs in a fresh browser context.

---

### Q27. How do you use environment variables?

```ts
process.env.BASE_URL
```

---

### Q28. How do you take screenshots?

```ts
await page.screenshot({ path: 'test.png' });
```

---

### Q29. How do you capture videos?

```ts
use: { video: 'on' }
```

---

### Q30. What is trace viewer?

Used to debug failed tests step-by-step.

```bash
npx playwright show-trace trace.zip
```

---

### Q31. How do you run tests in parallel?

```ts
workers: 4
```

---

### Q32. How do you tag tests?

```ts
test('smoke test @smoke', async () => {});
```

---

### Q33. How do you mock API responses?

```ts
await page.route('**/api/users', route =>
  route.fulfill({ json: mockData })
);
```

---

### Q34. How do you intercept network calls?

```ts
page.on('request', req => console.log(req.url()));
```

---

### Q35. How do you validate API response?

```ts
const response = await page.waitForResponse('**/api/users');
expect(response.status()).toBe(200);
```

---

## 🔴 ADVANCED QUESTIONS (36–50)

### Q36. How do you design a Playwright framework?

* Page Object Model
* Fixtures
* Config-driven environments
* CI integration

---

### Q37. What is POM?

Separates UI locators and actions from test logic.

---

### Q38. What are fixtures?

Reusable setup and teardown logic.

```ts
test.use({ storageState: 'auth.json' });
```

---

### Q39. How do you handle authentication?

```ts
await page.context().storageState({ path: 'auth.json' });
```

---

### Q40. How do you reduce flaky tests?

* Stable locators
* API mocks
* Retries
* Test isolation

---

### Q41. How do you handle dynamic elements?

Use role-based locators and assertions.

---

### Q42. How do you test APIs with Playwright?

```ts
const response = await request.get('/users');
```

---

### Q43. How do you integrate with CI/CD?

Using GitHub Actions / Jenkins.

---

### Q44. How do you run tests in Docker?

Using Playwright official Docker image.

---

### Q45. How do you debug failing tests?

* Headed mode
* Trace viewer
* Screenshots
* Logs

---

### Q46. How do you test responsive layouts?

```ts
use: { viewport: { width: 375, height: 812 } }
```

---

### Q47. How do you handle cookies?

```ts
await context.addCookies([]);
```

---

### Q48. How do you test mobile browsers?

```ts
devices['iPhone 13']
```

---

### Q49. How do you share test data?

Using fixtures or JSON files.

---

### Q50. What are Playwright reporters?

HTML, JSON, JUnit, Allure.

---

## 🧪 CODING QUESTIONS (51–55)

### Q51. Login test using getByRole

```ts
await page.getByRole('textbox', { name: 'Username' }).fill('admin');
await page.getByRole('textbox', { name: 'Password' }).fill('admin123');
await page.getByRole('button', { name: 'Login' }).click();
```

---

### Q52. Validate successful login

```ts
await expect(page.getByText('Logged In Successfully')).toBeVisible();
```

---

### Q53. Handle new tab

```ts
const [tab] = await Promise.all([
  context.waitForEvent('page'),
  page.click('a[target=_blank]')
]);
```

---

### Q54. Hard wait vs soft wait?

Hard wait blocks execution. Soft waits use auto-waiting.

---

### Q55. Validate table data

```ts
await expect(page.locator('table tr')).toHaveCount(5);
```

---

## 🗣️ MOCK INTERVIEW – HR ROUND

### Q: Tell me about yourself.

Automation Engineer with 3+ years of experience in Playwright, building scalable automation frameworks and mentoring juniors.

---

### Q: Why Playwright?

Fast execution, auto-waiting, modern APIs, cross-browser support.

---

## 🧠 MOCK INTERVIEW – TECHNICAL ROUND

### Q: How do you debug flaky tests?

Using trace viewer, role-based locators, retries, and API mocking.

---

### Q: Explain your framework design.

POM + fixtures + config-driven environments + CI integration.

---

## ⚙️ REAL-TIME SCENARIO QUESTIONS

### Q: Describe a real challenge you faced.

Flaky checkout tests due to dynamic DOM, solved using API mocks and stable locators.

---

### Q: How do you mentor juniors?

Code reviews, pair programming, documentation, and best practices.

---


