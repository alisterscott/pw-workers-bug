# pw-workers-bug

When limiting a project to a certain number of workers, the message "Running x tests on y workers" doesn't show the correct number of workers

Steps to reproduce bug:

1. `npx playwright test --project=firefox` shows two browsers which is correct and message "Running 2 tests using 2 workers" ✅
2. `npx playwright test --project=chromium` shows one browser which is correct but message "Running 2 tests using 2 workers" ❌ should be "Running 2 tests using 1 worker"
