# pw-workers-bug

When limiting a project to a certain number of workers, the message "Running x tests on y workers" doesn't show the correct number of workers

Steps to reproduce bug:

Given config https://playwright.dev/docs/api/class-testproject#test-project-workers

```
export default defineConfig({
  testDir: "./tests",
  fullyParallel: true,
  workers: 4,
  reporter: "html",
  use: {
    trace: "on-first-retry",
  },

  /* Configure projects for major browsers */
  projects: [
    {
      name: "chromium",
      use: { ...devices["Desktop Chrome"], headless: false },
      workers: 1,
    },

    {
      name: "firefox",
      use: { ...devices["Desktop Firefox"], headless: false },
    },
  ],
});
```

Running:

1. `npx playwright test --project=firefox` shows two browsers which is correct and message `Running 2 tests using 2 workers` which is correct ✅
2. `npx playwright test --project=chromium` shows one browser which is correct but message `Running 2 tests using 2 workers` ❌ should be `Running 2 tests using 1 worker` as only 1 worker is used
