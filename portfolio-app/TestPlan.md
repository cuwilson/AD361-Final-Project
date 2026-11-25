# Test Plan: Counter and Task Manager

This is my plan for testing two parts of my portfolio app. Both of them show up on the Home page.

| Part | File | What I will test |
|---|---|---|
| Counter | `src/components/Counter.tsx` | Static testing and white box testing |
| Task Manager | `src/components/TaskManager.tsx` (it also uses `src/hooks/useLocalStorage.ts`) | Black box testing |

Defect management and AI-assisted testing are used for both parts.

## 1. Test Objectives

What I want to find out from testing:

- Check that every button on the Counter does what it should: Increment, Increment Twice, Increment with Delay, Correct Increment Twice, and Reset.
- Find out why Increment Twice and Increment with Delay don't always add the right amount. They use `count` directly instead of `prevCount`, and I want to prove that Correct Increment Twice fixes this.
- Look for messy or risky code in Counter without running it.
- Make sure my tests run every line and every function in Counter.
- Check that Task Manager lets a user add tasks, mark them done, and still have them after the page reloads.
- See what Task Manager does with weird input like an empty task or a super long task.
- Write down every bug I find in the same way every time.
- See if AI can help me come up with tests, and make sure I still check its work.

## 2. Scope

### What is in scope
- Counter: how it looks when it loads, all five buttons, the count going up and resetting, the 2 second delay, and the CSS class names on the buttons.
- Task Manager: the list of tasks, the text box, the Add button, the Toggle button, the "Done" / "Not Done" label, and saving tasks in `localStorage` under the name `tasks`.
- Checking `Counter.tsx` with ESLint and TypeScript.

### What is out of scope
- Static and white box testing for Task Manager. I only test it as a black box.
- Black box testing for Counter, except what I need to help the white box tests.
- All the other components, the other pages, routing, and the json-server API.
- Speed tests, heavy load tests, and security tests.
- The inside of React itself.

## 3. Test Environment and Tools

| Thing | Details |
|---|---|
| Computer | Mac (macOS) |
| Software | Node.js (current LTS version) and npm |
| App is built with | React 19, TypeScript, and Vite |
| Browsers for black box | Chrome (main one), Firefox, and Safari (newest versions) |
| Static checking | ESLint (`npm run lint`) and TypeScript (`tsc -b`) |
| White box tools | Vitest, React Testing Library, user-event, Vitest fake timers, and v8 coverage (I still need to install these) |
| Black box tools | Testing by hand in the browser, using DevTools (Application tab) to see `localStorage`. Maybe a Playwright script later |
| Bug tracking | GitHub Issues |
| AI tools | Kiro and an AI chat assistant |

How I set things up:
- Clear `localStorage` before every Task Manager test so the list starts empty.
- Start the app with `npm run dev`.
- Use fake timers in the white box tests so I don't have to really wait 2 seconds each time.

## 4. Test Approach

I will test in this order:

1. **Static testing** of Counter first, before running anything.
2. **White box testing** of Counter. I can see the code, so I write tests that make sure every line and function runs.
3. **Black box testing** of Task Manager. I pretend I don't know the code and only use what I can see on the screen: the text box, the buttons, and the list.
4. **Defect management** for every problem I find.
5. **AI-assisted testing** to get extra test ideas, and then I check them myself.

When a bug gets fixed I test it again. Then I run all the tests again to make sure the fix didn't break something else.

## 5. Risks

| Risk | How likely | How bad | What I will do about it |
|---|---|---|---|
| The "Increment Twice" and "Increment with Delay" buttons might be on purpose to show a React problem (the Increment Twice button is even marked with a warning). Someone might call them bugs by mistake. | High | Medium | Write down what is supposed to happen: Increment Twice adds 1, and Correct Increment Twice adds 2. Mark it as "known behavior" if it is a teaching demo. |
| I haven't installed a test tool yet | High | Medium | Install Vitest and Testing Library before starting white box tests. |
| The 2 second delay test might not work the same every time | Medium | Medium | Use fake timers in the automatic tests. For hand tests, use a stopwatch and allow about half a second either way. |
| Task Manager has no written rules, so I'm not sure what should happen with empty or repeated tasks | High | Medium | Decide the right answers before testing and write them in the test cases. |
| Old data in `localStorage` can mess up the next test | Medium | Medium | Clear it before each test. |
| `useLocalStorage` uses `JSON.parse` with no protection, so bad saved data could crash the page | Medium | High | Add a test where I change the saved `tasks` data to something broken. |
| Task ids come from `Date.now()`, so two tasks added at the same exact millisecond could get the same id | Low | Medium | Add a test where I click Add really fast. |
| AI might write tests that are wrong or that just copy what the code does now | Medium | High | Read every AI test and compare it to what the app should do. |
| Not enough time | Medium | Medium | Test the most important stuff first (state updates, saving, empty input). |

## 6. Entry and Exit Criteria

### Entry criteria (what must be true before I start)
- `npm install` and `npm run build` finish with no errors.
- The app runs with `npm run dev` and the Home page shows Counter and Task Manager.
- The test tools for white box testing are installed.
- I wrote down what each Counter button and each Task Manager action should do.
- The test cases are written and checked.

### Exit criteria (what must be true before I'm done)
- Every planned test case has been run and the results are written down.
- ESLint and `tsc` show no errors for `Counter.tsx`, or I explain each leftover warning.
- Counter has 100% statement coverage and 100% function coverage, and every branch that exists is covered.
- No critical or high bugs are still open.
- Any medium or low bugs left open are written down and accepted.
- The re-run of all tests passes.
- The test summary report is finished.

## 7. Test Deliverables

### 7.1 Static Testing (Counter)

**What I will do:**
- Run `npm run lint` and `tsc -b` and write down what they say about `Counter.tsx`.
- Read through the code with this checklist:
  - When the new count depends on the old count, does the code use `setCount(prev => prev + 1)`?
  - `incrementTwice` calls `setCount(count + 1)` two times. React batches them, and both use the same `count`, so it only goes up by 1.
  - `incrementDelay` remembers `count` from when the button was clicked. If you click it and then click Increment during the 2 seconds, one of the updates is lost.
  - Does the timer get cleared if the component goes away? (`incrementDelay` never saves or clears its timer.)
  - Are the handler names and button labels clear and matching?
  - Is the `warning-btn` class actually in the CSS file that gets imported?
  - Is the code style consistent? (Some lines have semicolons and some don't.)
  - Can a screen reader tell when the count changes? (There is no `aria-live` area.)
  - Are both `App.css` and `Counter.css` needed?

**What I will hand in:**
- The ESLint and `tsc` results for `Counter.tsx`.
- The finished checklist with what I found and how serious each thing is.
- A list of which problems got fixed and which were left for later.

### 7.2 Black Box Testing (Task Manager)

**Ways I will test:** equivalence partitioning (grouping similar inputs), boundary value analysis (testing the edges), state transition testing, and exploratory testing (just trying things out).

**Planned test cases:**

| ID | What I'm testing | Steps | What should happen |
|---|---|---|---|
| TM-01 | Starting screen | Clear `localStorage`, load Home | The "Tasks" heading shows and the list is empty |
| TM-02 | Add a normal task | Type "Buy milk", click Add | The task shows up as "Not Done" and the text box clears |
| TM-03 | Add a few tasks | Add three tasks | All three show in the order I added them |
| TM-04 | Mark as done | Click Toggle on a task | The label changes to "Done" and the text looks completed |
| TM-05 | Undo done | Click Toggle again | The label goes back to "Not Done" |
| TM-06 | Toggle just one | Toggle the second of three tasks | Only that task changes |
| TM-07 | Empty text box | Click Add with nothing typed | A task should NOT be added (I need to confirm this, because the code looks like it adds a blank one) |
| TM-08 | Only spaces | Type three spaces, click Add | A task should NOT be added (confirm) |
| TM-09 | Really long title | Add a title with 500 characters | The task is added and the page layout doesn't break |
| TM-10 | Special characters | Add `<b>test</b>` and `"quotes" & symbols` | The text shows exactly as typed, not as HTML |
| TM-11 | Same title twice | Add "Task" two times | Both show up and each can be toggled by itself |
| TM-12 | Saving | Add two tasks, toggle one, reload the page | The tasks and their done status are still there |
| TM-13 | Saving after closing | Do TM-12, but close the tab and open it again | Same as TM-12 |
| TM-14 | Broken saved data | Change `tasks` in `localStorage` to `{bad`, reload | The page shouldn't crash (confirm) |
| TM-15 | Enter key | Type a task and press Enter | Write down whether it adds the task (the code only has a click handler) |
| TM-16 | Clicking fast | Click Add quickly many times with text in the box | Each task is added one time with its own entry |
| TM-17 | Different screen sizes | Look at 375, 768, and 1280 px wide | The list, text box, and buttons still work |
| TM-18 | Keyboard only | Use Tab to move through the box and buttons and press Space | I can reach everything and it works |

**What I will hand in:**
- The test case document (this table, plus the actual results and pass or fail).
- A log of each run with the date, browser, and who tested.
- Notes from my exploratory testing.
- Screenshots for any test that fails.

### 7.3 White Box Testing (Counter)

**Ways I will test:** statement coverage, function coverage, and checking how state updates work. I will write unit tests with Vitest and React Testing Library.

**Planned test cases:**

| ID | What I'm testing | Test | What should happen |
|---|---|---|---|
| CW-01 | First render | Render `<Counter />` | The heading says "Counter: 0" and there are five buttons |
| CW-02 | `increment` | Click Increment one time | Count is 1 |
| CW-03 | `increment` | Click Increment three times | Count is 3 |
| CW-04 | `incrementTwice` | Click Increment Twice starting at 0 | Count is 1 (not 2) because both calls use the same `count` |
| CW-05 | `incrementTwiceCorrectly` | Click Correct Increment Twice starting at 0 | Count is 2 |
| CW-06 | `incrementDelay` | Click Increment with Delay and check right away | Count is still 0 |
| CW-07 | `incrementDelay` | Click it, then move the fake timers forward 2000 ms | Count is 1 |
| CW-08 | `incrementDelay` | Click it, then move the timers forward only 1999 ms | Count is still 0 (edge case) |
| CW-09 | `incrementDelay` old value problem | Click Increment with Delay, then click Increment, then move timers forward 2000 ms | Count is 1 (not 2) because the delayed update uses the old `count` |
| CW-10 | `reset` | Increment up to 3, then click Reset | Count is 0 |
| CW-11 | `reset` | Click Reset when it's already 0 | Count stays 0 |
| CW-12 | Mixed buttons | Increment, Correct Increment Twice, Reset, Increment | Count is 1 |
| CW-13 | Unmounting | Click Increment with Delay, remove the component, move timers forward | No error happens |

**Coverage goals:** 100% statements, 100% functions, and 100% lines for `Counter.tsx`. The component has no if-statements, so branch coverage is 100% as long as every handler runs.

**What I will hand in:**
- The automatic test file (for example `src/components/Counter.test.tsx`) saved in the project.
- The coverage report (HTML and a text summary).
- A written explanation of the results of the old-value tests (CW-04 and CW-09).

### 7.4 Defect Management

**How it works:** Log it, triage it (decide how bad it is), assign it, fix it, retest it, and close it. Every bug from static, white box, and black box testing goes into GitHub Issues.

**What each bug report needs:** ID, title, which part it's in, test case ID, description, steps to make it happen, what should happen, what really happened, severity, priority, environment (browser and version), screenshot or log, status, and owner.

| Severity | What it means |
|---|---|
| Critical | The page crashes or data is lost, and there is no way around it |
| High | A main feature doesn't work and it's hard to get around |
| Medium | A feature only partly works, but there is a way around it |
| Low | Small or looks-only problem |

**Statuses:** New, Open, In Progress, Fixed, Retest, Closed, Reopened, Deferred.

**What I will hand in:**
- The bug list in GitHub Issues.
- A bug summary report with counts by severity, status, part of the app, and kind of test (static, white box, black box).
- Retest and re-run results for every bug that gets fixed.

### 7.5 AI-Assisted Testing

**How I will use AI:**
- Give the AI the Counter code and ask for edge cases and Vitest tests, then compare them with CW-01 to CW-13.
- Describe what Task Manager looks like and does (without showing the code) and ask for black box test cases, then compare them with TM-01 to TM-18.
- Ask the AI to review `Counter.tsx` for old-value and cleanup problems, then compare that with my own static review.
- Ask the AI to turn my rough notes into clear bug reports.

**Rules I will follow:**
- I read, run, and fix every AI test before I save it in the project.
- I check each test against what the app is supposed to do, not just what the code does now. For example, if the AI writes a test that says Increment Twice reaches 2, the test will fail, and I need to figure out why instead of just changing it to pass.
- Mutation check: I will change the code on purpose (like changing `+ 1` to `+ 2`) and make sure the AI tests fail.
- I won't share passwords or personal info with AI tools.

**What I will hand in:**
- A log of my prompts and the answers, marked as accepted, edited, or rejected.
- The AI-assisted tests, labeled so people know they came from AI.
- A comparison of AI-assisted and hand testing: how many good test cases, bugs found, wrong suggestions, and time spent.
- A short reflection on what AI is good at, where it falls short, and what I recommend.
