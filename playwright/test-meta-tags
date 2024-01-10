### Extract Meta Tags and Assert using Playwright

1. Find meta tags on the page by visiting `View Page Sourse` or by navigatig to the Elements tab in Developer Tools in Chrome. 

2. Extract meta tags using Playwright and assert:

```
const { test, expect } = require(‘@playwright/test’);

test(‘basic test’, async ({ page }) => {
    await page.goto(‘https://your-site.com’);
    const metaDescription = page.locator(‘meta[name=“description”]’);
    await expect(metaDescription).toHaveAttribute(‘content’, ‘something’)
});
```
