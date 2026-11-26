# Test Plan: Counter and Task Manager

## Project Overview

The application being tested is a React portfolio application originally developed for AD312. It demonstrates React development concepts, including component state management, user interactions, form validation, data persistence, and asynchronous updates.

This test plan focuses on two components located on the Home page.

| Component | File | Testing Types |
|---|---|---|
| Counter | `src/components/Counter.tsx` | Static and white-box testing |
| Task Manager | `src/components/TaskManager.tsx` | Static, black-box, and white-box testing |
| Local Storage Hook | `src/hooks/useLocalStorage.ts` | Static and white-box testing |

Defect management and AI-assisted testing will be used throughout the testing process.

### Team Responsibilities

| Activity | Assigned To |
|---|---|
| Initial test plan | Cole |
| Test plan review | Both |
| Static testing | Cole |
| Black-box testing | Copper |
| White-box testing | Copper |
| Initial defect reporting | Cole |
| Defect corrections | Copper |
| Confirmation testing | Copper |
| Regression testing | Copper |
| AI-assisted testing | Both |
| Final documentation review | Both |
| Presentation and demonstration | Both |

## 1. Test Objectives

- Verify that each Counter button performs its intended behavior.
- Verify that the Counter correctly demonstrates the differences between direct and functional React state updates.
- Identify unintended defects, risky code, and opportunities for improvement through static testing.
- Verify that the Task Manager allows users to add tasks and toggle their completion status.
- Verify that tasks and their completion statuses persist after the page reloads.
- Evaluate how the Task Manager handles valid, invalid, and unexpected inputs.
- Achieve meaningful statement, branch, function, and iteration coverage within the selected components.
- Identify, document, correct, and retest genuine application defects.
- Use AI-assisted testing to improve test design, code review, and defect documentation while independently verifying its recommendations.

## 2. Scope

### In Scope

**Counter**
- Initial counter value.
- Increment button.
- Increment Twice button.
- Correct Increment Twice button.
- Increment with Delay button.
- Reset button.
- Asynchronous state updates.
- Intentional demonstrations of incorrect React state handling.
- Source-code quality and maintainability.

**Task Manager**
- Initial task list.
- Adding tasks.
- Task input validation.
- Toggling task completion.
- Managing multiple tasks.
- Handling duplicate task titles.
- Displaying special characters and long task titles.
- Task persistence after refreshing or reopening the application.
- Handling unexpected or corrupted saved data.
- Basic responsive behavior and keyboard interactions.

**Local Storage Hook**
- Initialization with and without existing saved data.
- Reading and writing saved data.
- Handling invalid saved data.

### Out of Scope

- Other portfolio components and pages.
- Application routing.
- JSON Server API.
- Comprehensive performance and load testing.
- Comprehensive security testing.
- Internal implementation of React and third-party libraries.
- Correcting intentionally incorrect code used for educational demonstrations.

### Expected Behavior

The following expected behaviors will be reviewed and agreed upon by both team members before testing begins.

| Feature | Expected Behavior |
|---|---|
| Counter initialization | Counter starts at 0 |
| Increment | Increases the counter by 1 |
| Increment Twice | Increases the counter by 1 as an intentional demonstration of incorrect React state handling |
| Correct Increment Twice | Increases the counter by 2 |
| Increment with Delay | Increases the counter by 1 after two seconds when tested independently |
| Reset | Returns the counter to 0 |
| Valid task input | Adds a new task with a status of Not Done |
| Empty or whitespace-only task input | Does not add a task |
| Duplicate task titles | Tasks are allowed and can be managed independently |
| Task completion | Toggle changes only the selected task's completion status |
| Task persistence | Tasks and completion statuses remain after reloading |
| Invalid saved data | Application handles invalid data without crashing |

The expected behavior of delayed updates combined with other Counter actions will be reviewed to determine whether the behavior is intentional or unintended.

Intentional educational behavior will be documented but will not be classified as a defect.

## 3. Test Environment and Tools

| Requirement | Details |
|---|---|
| Operating systems | macOS and Windows |
| Software | Node.js and npm |
| Application technologies | React, TypeScript, and Vite |
| Browsers | Chrome, Firefox, and Safari where available |
| Static testing tools | Manual code review, ESLint, and TypeScript |
| White-box testing tools | Vitest, React Testing Library, user-event, jsdom, fake timers, and V8 coverage |
| Black-box testing tools | Manual browser testing and browser DevTools |
| Defect tracking | GitHub Issues |
| Version control | Git and GitHub |
| AI tools | Kiro and ChatGPT |

### Environment Setup

- Navigate to the `portfolio-app` directory.
- Install application dependencies using `npm install`.
- Start the application using `npm run dev`.
- Install and configure the required automated testing libraries.
- Clear relevant Task Manager localStorage data before independent tests.
- Use fake timers when testing delayed Counter updates.
- Record the operating system, browser, and application version or commit used during testing.

## 4. Test Approach

Testing will be completed using the following approaches.

| Testing Activity | Approach | Assigned To |
|---|---|---|
| Static testing | Manual source-code review and automated static analysis | Cole |
| Black-box testing | Equivalence partitioning, state transition testing, and exploratory testing | Copper |
| White-box testing | Automated statement, branch, function, and iteration testing | Copper |
| Defect management | Document and prioritize discovered defects | Cole |
| Defect correction | Modify application code to resolve confirmed defects | Copper |
| Confirmation testing | Repeat tests related to corrected defects | Copper |
| Regression testing | Repeat relevant tests to verify existing functionality | Copper |
| AI-assisted testing | Use focused prompts to support testing activities | Both |

Testing activities may occur in parallel. Findings will be communicated between both team members throughout the project.

When a defect is identified, it will be documented before changes are made to the application. After the correction is completed, confirmation testing and regression testing will be performed.

## 5. Risks

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Intentional Counter behavior is incorrectly classified as a defect | High | Medium | Document the educational purpose and expected behavior before testing |
| Automated testing tools are not yet configured | High | Medium | Install and configure the testing environment before executing automated tests |
| Delayed Counter tests produce inconsistent results | Medium | Medium | Use fake timers for automated testing |
| Task Manager has incomplete documented input requirements | High | Medium | Agree on expected behavior before executing tests |
| Existing localStorage data interferes with test results | Medium | Medium | Reset relevant saved data between independent tests |
| Invalid saved data causes the application to crash | Medium | High | Test corrupted localStorage data and document confirmed failures |
| Tasks receive duplicate identifiers | Low | Medium | Verify that tasks can be managed independently when added rapidly |
| Application changes introduce additional defects | Medium | High | Perform confirmation and regression testing after corrections |
| AI-generated tests contain incorrect assumptions | Medium | High | Independently review and verify AI-generated recommendations |
| Limited time prevents completion of testing | Medium | Medium | Prioritize required testing techniques and core functionality |
| Concurrent changes create merge conflicts | Medium | Medium | Communicate changes and use separate branches and pull requests |

## 6. Entry and Exit Criteria

### Entry Criteria

- The application is available in the shared GitHub repository.
- Application dependencies are installed.
- The application can run in the local development environment.
- The selected components are accessible.
- Required testing tools are installed and configured before their respective testing activities.
- Expected application behaviors are documented and reviewed.
- Test cases are prepared before execution.
- Team responsibilities are assigned.

Existing build or static analysis errors will be documented rather than preventing static testing from beginning.

### Exit Criteria

- Manual and automated static testing are completed.
- At least two black-box testing techniques are applied.
- At least six black-box test cases are executed and documented.
- At least four automated white-box test cases are executed and documented.
- Statement and branch testing are completed, including iteration testing where applicable.
- A code coverage report is generated.
- At least two defect reports are completed.
- Corrected defects have been retested.
- Regression testing is completed.
- No unresolved critical or high-severity defects remain without documented justification.
- At least three focused uses of AI-assisted testing are documented.
- All required testing documentation is committed to the shared repository.
- Both team members have contributed commits and pull requests.
- The final test summary, presentation, and partner contribution summary are completed.

## 7. Test Deliverables

### 7.1 Static Testing

**Assigned to: Cole**

Manual and automated static testing will be performed on the selected source-code files.

#### Manual Review

The review will evaluate:

- Correct use of React state updates.
- Intentional and unintentional incorrect behavior.
- Asynchronous timer management.
- Task input validation.
- Task identifier generation.
- Handling of invalid localStorage data.
- Code readability and consistency.
- Accessibility of interactive components.
- Error handling.

Intentional examples of incorrect React state handling will be documented separately from genuine defects.

#### Automated Static Analysis

The following commands will be used from the `portfolio-app` directory:

- `npm run lint`
- `npx tsc -b`

Results relating to the selected components will be documented. Findings outside the testing scope may be noted separately.

#### Deliverables

- Manual code review checklist.
- Automated static analysis results.
- Identified findings and recommended corrections.
- Severity and final status of confirmed defects.
- Evidence of corrections made.
- Updated analysis results following corrections.

### 7.2 Black-Box Testing

**Assigned to: Copper**

Black-box testing will focus on the Task Manager's observable behavior without relying on its internal implementation to determine expected results.

The primary techniques will be:

- Equivalence partitioning.
- State transition testing.

Exploratory testing will also be used to evaluate additional application behaviors.

#### Equivalence Partitioning

| Classification | Partition | Expected Result |
|---|---|---|
| Task input | Valid, non-empty title | Task is added |
| Task input | Empty title | Task is not added |
| Task input | Whitespace-only title | Task is not added |
| Task input | Special characters | Task is displayed as text |
| Task title duplication | Unique title | Task is added |
| Task title duplication | Duplicate title | Task is added and managed independently |

#### State Transition Testing

| Current State | Action | Expected State |
|---|---|---|
| No task | Add valid task | Not Done |
| No task | Add invalid task | No task |
| Not Done | Toggle | Done |
| Done | Toggle | Not Done |
| Not Done | Reload application | Not Done |
| Done | Reload application | Done |

#### Planned Test Cases

| ID | Test Scenario | Expected Result |
|---|---|---|
| TM-01 | Load Task Manager without saved tasks | Task list is empty |
| TM-02 | Add a normal task | Task appears as Not Done and input clears |
| TM-03 | Add three different tasks | All three tasks appear |
| TM-04 | Toggle an incomplete task | Status changes to Done |
| TM-05 | Toggle a completed task | Status changes to Not Done |
| TM-06 | Toggle one of three tasks | Only the selected task changes |
| TM-07 | Add an empty task | No task is added |
| TM-08 | Add a whitespace-only task | No task is added |
| TM-09 | Add a 500-character task title | Task is displayed without making the interface unusable |
| TM-10 | Add special characters and HTML-like text | Input is displayed as text |
| TM-11 | Add the same title twice | Both tasks appear and can be managed independently |
| TM-12 | Add tasks, toggle one, and reload | Tasks and statuses persist |
| TM-13 | Close and reopen the application at the same URL | Tasks and statuses persist |
| TM-14 | Load with corrupted saved task data | Application handles invalid data without crashing |
| TM-15 | Enter a task and press Enter | Observe and document keyboard behavior |
| TM-16 | Rapidly add multiple valid tasks | Tasks are created as independent entries |
| TM-17 | Test different screen sizes | Task Manager remains usable |
| TM-18 | Navigate and operate controls using the keyboard | Input and buttons remain accessible |

TM-15 will be treated as an exploratory scenario unless a specific keyboard submission requirement is established.

#### Deliverables

- Equivalence partition tables.
- State transition table.
- Test cases with steps, expected results, actual results, and pass or fail status.
- Exploratory testing notes.
- Evidence of failed tests.
- Confirmation testing results following corrections.

### 7.3 White-Box Testing

**Assigned to: Copper**

Automated white-box testing will focus on Counter, Task Manager, and the localStorage hook.

Tests will be created using Vitest and React Testing Library based on the internal implementation of the selected components.

#### Testing Techniques

| Technique | Application |
|---|---|
| Statement testing | Execute statements within the selected components and hook |
| Branch testing | Test conditional outcomes in Task Manager and the localStorage hook |
| Iteration testing | Test task-list operations with zero, one, and multiple tasks |
| Function testing | Execute Counter and Task Manager event handlers |
| Asynchronous testing | Verify delayed Counter updates using fake timers |

#### Planned Counter Test Cases

| ID | Test Scenario | Expected Result |
|---|---|---|
| CW-01 | Initial render | Counter displays 0 |
| CW-02 | Increment once | Counter displays 1 |
| CW-03 | Increment three times | Counter displays 3 |
| CW-04 | Click Increment Twice | Counter displays 1 as intentionally demonstrated |
| CW-05 | Click Correct Increment Twice | Counter displays 2 |
| CW-06 | Click Increment with Delay | Counter remains unchanged immediately |
| CW-07 | Advance timer by 2000 ms | Counter increases by 1 |
| CW-08 | Advance timer by 1999 ms | Counter remains unchanged |
| CW-09 | Increment during a pending delayed update | Document behavior and compare against agreed expectations |
| CW-10 | Reset a non-zero counter | Counter displays 0 |
| CW-11 | Reset a counter already at 0 | Counter remains at 0 |
| CW-12 | Execute multiple different Counter actions | Counter reflects the expected sequence |
| CW-13 | Unmount with a pending delayed update | No unintended errors or effects occur |

#### Planned Task Manager and Local Storage Test Cases

| ID | Test Scenario | Technique | Expected Result |
|---|---|---|---|
| TW-01 | Initialize without saved tasks | Branch | Empty task list is displayed |
| TW-02 | Initialize with saved tasks | Branch | Saved tasks are restored |
| TW-03 | Add a valid task | Statement | Task is added |
| TW-04 | Add an invalid task | Statement / Branch | Task is rejected |
| TW-05 | Toggle a task with multiple tasks present | Branch | Matching task changes and other tasks remain unchanged |
| TW-06 | Render zero tasks | Iteration | No task entries are rendered |
| TW-07 | Render one task | Iteration | One task entry is rendered |
| TW-08 | Render multiple tasks | Iteration | All task entries are rendered |
| TW-09 | Update task completion | Statement | Updated task data is saved |
| TW-10 | Initialize with malformed saved data | Error handling | Invalid data is handled without crashing |

#### Coverage Goals

| Coverage Type | Target |
|---|---|
| Statement coverage | 94% or higher |
| Line coverage | 94% or higher |
| Function coverage | 100% |
| Branch coverage | 100% of applicable branches where feasible |
| Iteration testing | Zero, one, and multiple iterations where applicable |

Coverage goals apply to the selected source-code files rather than the entire portfolio application. Any unmet targets will be documented and explained.

#### Deliverables

- Automated test files.
- Automated test execution results.
- Code coverage report.
- Explanation of statement, branch, and iteration testing.
- Documentation of failed tests.
- Confirmation and regression testing results.

### 7.4 Defect Management

**Initial defect reporting: Cole**

**Defect corrections and retesting: Copper**

Genuine defects discovered during static, black-box, and white-box testing will be documented using GitHub Issues.

Intentional educational examples will not be reported as defects unless their behavior differs from their documented educational purpose.

Potential areas for defect investigation include:

- Empty or whitespace-only tasks being accepted.
- Invalid localStorage data causing application crashes.
- Duplicate task identifiers causing incorrect task updates.
- Unintended asynchronous state updates.
- Input handling and display issues.

These are potential findings and will only be classified as confirmed defects after review or testing.

#### Defect Report Requirements

Each defect report will include:

- Defect ID and title.
- Related test case or static review.
- Test environment.
- Steps to reproduce or source-code location.
- Expected result.
- Actual result.
- Severity.
- Priority.
- Assigned owner.
- Supporting evidence.
- Current status.

#### Severity Classification

| Severity | Description |
|---|---|
| Critical | Application crashes or significant data loss occurs without a reasonable workaround |
| High | A core application feature does not function correctly |
| Medium | A feature functions incorrectly but remains partially usable or has a workaround |
| Low | Minor visual, usability, or non-critical issue |

#### Priority Classification

| Priority | Description |
|---|---|
| High | Correction should be completed before project completion |
| Medium | Correction should be completed when resources allow |
| Low | Correction may be deferred with documentation |

#### Defect Workflow

1. Identify and reproduce the defect.
2. Cole creates the initial defect report.
3. Review and assign severity and priority.
4. Assign the defect to Copper.
5. Copper implements the correction.
6. Perform confirmation testing.
7. Perform regression testing.
8. Close or reopen the defect based on the results.

At least two defect reports will be completed. Genuine defects will be prioritized. If insufficient genuine defects are discovered, a controlled defect may be introduced and documented as an intentionally seeded defect in accordance with the instructor's guidance.

#### Deliverables

- At least two completed defect reports.
- Supporting screenshots, logs, or code references.
- Evidence of corrections.
- Confirmation testing results.
- Regression testing results.
- Final defect statuses.

### 7.5 AI-Assisted Testing

**Assigned to: Both**

AI tools will be used to support testing activities throughout the project.

Planned uses include:

| AI-Assisted Activity | Purpose |
|---|---|
| Static code review | Identify potential code-quality issues and unintended behavior |
| Black-box test design | Identify equivalence partitions, state transitions, and unexpected inputs |
| White-box test design | Identify statements, branches, iteration scenarios, and coverage gaps |
| Defect documentation | Improve the clarity and completeness of defect reports |

All AI-generated recommendations will be independently reviewed and verified before being used.

AI will not be used to generate or fabricate actual test results.

For each documented AI interaction, the following information will be recorded:

- Complete prompt.
- Testing activity supported.
- Context provided to the AI.
- How the response was used.
- Recommendations accepted, revised, or rejected.

#### Deliverables

- At least three focused AI-assisted testing interactions.
- Complete prompts and relevant responses.
- Explanation of how AI recommendations were verified.
- Documentation of accepted, revised, and rejected recommendations.

**This document was edited for clarity and formating with the use of AI**