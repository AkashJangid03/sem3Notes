# Software Testing — Solved Question Paper
**M.Sc. Computer Applications — Semester III**  
**CSA603: Software Testing | NEP 2020 Pattern**  
**Time: 2 Hours | Maximum Marks: 60**

> Answers cover all questions visible across the two uploaded page images. The paper says “Any” for each section; all visible options are answered for revision.

---

# Q1. Answer the following questions (Any Six) — 2 marks each

## (a) List any four purposes of Software Testing.
1. To detect defects in software.
2. To verify that software meets specified requirements.
3. To validate that software meets user needs.
4. To provide information about software quality and reduce the risk of failures after release.

## (b) Define Test Policy.
A **Test Policy** is a high-level document that states an organization's overall principles, objectives and approach to software testing. It provides direction for testing practices across projects.

## (c) Why Software Testing?
Software testing is performed to:
- Find defects before release.
- Check whether requirements have been implemented correctly.
- Compare actual results with expected results.
- Assess reliability, security, performance and other quality attributes.
- Reduce the risk and cost of failures in production.

## (d) Write the post-condition of Undergraduate Admission System.
A **post-condition** is the state expected after an operation or test has completed.

For a successful undergraduate admission application, possible post-conditions are:
- The student's application/admission record is saved.
- The student's details and selected course are recorded correctly.
- An application/admission number or confirmation is generated.
- The application status is updated, for example to *Submitted* or *Admitted*.

*The question does not specify the exact operation, so these are examples rather than a fixed source-provided answer.*

## (e) List the domains from Insurance System.
The wording may refer to domains/modules within an insurance system. Common examples are:
1. Policy management
2. Premium calculation and payment
3. Claims processing
4. Customer/member management
5. Agent/broker management
6. Policy renewal and servicing

*The image does not show the lecturer's exact list. Use the terminology in your lecture notes if it differs.*

## (f) What is Test Analysis?
**Test Analysis** is the activity of examining the test basis—such as requirements, specifications and design documents—to identify what needs to be tested and define test conditions. It helps establish test coverage and provides input for test case design.

## (g) List the frameworks used in Automation Testing.
Common automation testing frameworks include:
1. Linear / Record-and-Playback Framework
2. Modular Testing Framework
3. Data-Driven Framework
4. Keyword-Driven Framework
5. Hybrid Framework
6. Behaviour-Driven Development (BDD) Framework

*Framework classifications vary across course materials; match the list to your lecture notes.*

---

# Q2. Answer the following questions (Any Four) — 3 marks each

## (a) What is Automation Testing? Discuss any two benefits.
**Automation Testing** uses tools and test scripts to execute test cases, compare actual results with expected results and report outcomes with limited manual intervention.

**Two benefits:**
1. **Faster repeated execution:** Automated tests can be run repeatedly and are useful for regression testing after code changes.
2. **Consistency:** Scripts execute the same defined steps each time, reducing variation caused by manual repetition.

## (b) Explain advantages of Test Documentation in detail.
1. **Clear guidance:** Test plans and test cases define what to test, how to test it and expected results.
2. **Improved coverage:** Requirement-to-test links help identify requirements without test cases.
3. **Planning and estimation:** Documentation helps estimate effort, schedule, resources and testing scope.
4. **Better communication:** Testers, developers, managers and stakeholders share a common record.
5. **Repeatability:** Other testers can repeat documented steps and compare results.
6. **Defect tracking:** Execution records and defect reports preserve evidence and status.
7. **Training and maintenance:** New team members can understand the test approach and repeat checks after changes.

## (c) What is State Transition Testing? Explain in short.
**State Transition Testing** is a black-box testing technique used when a system's response depends on its current state and an event/input. It checks valid and invalid transitions between states.

**Example — login system:**
```text
        Correct credentials
  +------------------------------+
  |                              v
[Logged Out] --------------> [Logged In]
      |
      | repeated incorrect attempts
      v
   [Locked]
      |
      | recovery/unlock process
      v
 [Logged Out]
```
Test cases should cover allowed transitions, such as successful login, and restricted transitions, such as attempting to log in while locked.

## (d) Write a note on Telecom Domain.
Telecom domain testing checks telecom applications and services to ensure that customer, network, service and billing functions work as specified.

Common areas include:
- **Subscriber/customer management:** Registration, profile updates and account status.
- **Service activation:** Activating, changing or cancelling a plan.
- **Billing and charging:** Correct calculation of usage charges, plans, taxes and bills.
- **Call/data usage records:** Correct recording of voice, SMS and data usage.
- **Network/service availability:** Correct behaviour during interruptions and recovery.
- **Performance:** Handling expected transaction volumes and user load.

*These are general examples; the image does not include a detailed telecom checklist.*

## (e) Discuss Agile Testing Strategies in detail.
An **Agile testing strategy** integrates testing into every iteration and encourages continuous feedback and collaboration.

1. **Early involvement:** Testers participate in requirement discussions and iteration planning.
2. **Clear acceptance criteria:** Requirements are expressed in testable terms.
3. **Continuous testing:** Testing occurs throughout the iteration, not only after development finishes.
4. **Automation where appropriate:** Stable, repeatable tests—especially regression tests—can be automated.
5. **Regression testing:** Existing functionality is rechecked after changes.
6. **Collaboration:** Testers, developers, product owners and stakeholders discuss risks and results.
7. **Defect prioritization:** Defects are assessed by impact and urgency.
8. **Feedback and adaptation:** Test results, demonstrations and retrospectives help improve the product and next iteration.

---

# Q3. Answer the following questions (Any Three) — 4 marks each

## (a) Apply Boundary Value Analysis for a system accepting age from 18 to 75. Find the nominal value. Write 5 valid and invalid test cases.
The allowed age range is **18–75 inclusive**.

In **Boundary Value Analysis (BVA)**, values at and near the boundaries are tested because errors commonly occur at range limits.
- Lower boundary values: **17, 18, 19**
- Upper boundary values: **74, 75, 76**
- **Nominal value:** 30 (a typical value inside the valid range)

| ID | Age | Type | Expected result |
|---|---:|---|---|
| TC01 | 18 | Valid — lower boundary | Accepted |
| TC02 | 19 | Valid — just above lower boundary | Accepted |
| TC03 | 30 | Valid — nominal value | Accepted |
| TC04 | 74 | Valid — just below upper boundary | Accepted |
| TC05 | 75 | Valid — upper boundary | Accepted |
| TC06 | 17 | Invalid — below minimum | Rejected |
| TC07 | 16 | Invalid — below minimum | Rejected |
| TC08 | 76 | Invalid — above maximum | Rejected |
| TC09 | 77 | Invalid — above maximum | Rejected |
| TC10 | 0 | Invalid — outside range | Rejected |

## (b) Explain different types of defects with example.
A **defect** is a flaw in a software work product that may cause the system to behave differently from the expected result.

1. **Functional defect:** A feature does not work as required. *Example:* Clicking “Submit” does not save the admission form.
2. **Logical defect:** The program uses incorrect logic or a formula. *Example:* A discount is subtracted twice.
3. **User Interface (UI) defect:** A visual element or layout is incorrect. *Example:* A button overlaps form text.
4. **Performance defect:** The application responds too slowly or cannot handle expected load. *Example:* Search takes 20 seconds under normal load.
5. **Security defect:** A weakness allows unauthorized access or data exposure. *Example:* A user can view another user's private record by changing an ID in the URL.
6. **Compatibility defect:** Software behaves incorrectly on a supported browser, device or OS. *Example:* A form fails in a supported browser.
7. **Validation defect:** Incorrect input is accepted or valid input is rejected. *Example:* The system accepts an age below the specified minimum.

## (c) Predict the challenges in e-Commerce Domain.
1. **High traffic and scalability:** The website must remain responsive during sales and peak traffic.
2. **Payment gateway integration:** Payments, declines, cancellations and retries must be handled correctly.
3. **Security and privacy:** Customer and payment-related data must be protected.
4. **Cart and order consistency:** Prices, quantities, discounts, taxes, shipping and totals must be correct.
5. **Inventory synchronization:** An unavailable product should not be sold.
6. **Cross-browser/device compatibility:** Checkout should work across supported browsers and devices.
7. **Session management:** Cart/session information should behave correctly on expiry, logout and return visits.
8. **Order/refund workflows:** Confirmation, tracking, cancellation and refunds should update correctly.
9. **Internationalization:** Currency, language, date and regional rules may differ by market.

## (d) Write a note on Behaviour-Driven Development (BDD).
**Behaviour-Driven Development (BDD)** describes expected system behaviour in shared language so business stakeholders, testers and developers can agree on what the software should do.

BDD commonly uses **Given–When–Then**:
- **Given:** Initial context or preconditions.
- **When:** An action or event occurs.
- **Then:** The expected observable result.

**Example — admission application:**
```text
Given a student has completed all required fields
When the student submits the admission application
Then the system saves the application and displays a confirmation number
```

**Benefits:** Improves communication, clarifies acceptance criteria, reduces misunderstandings and provides concrete scenarios that can be checked during testing.

---

# Q4. Answer the following questions (Any Two) — 4 marks each

## (a) Justify: Manual Testing needs more investment in human resources than Automation Testing.
The statement is **generally true for repetitive, large-scale testing**, although automation requires initial investment in tools, scripts and maintenance.

1. **Manual execution:** Testers perform each step and check results themselves.
2. **Repeated effort:** Regression tests may need to be run after many code changes, increasing tester-hours.
3. **Limited parallel execution:** Manual testing can require more people to test many scenarios at once.
4. **Automation reduces repetition:** Once reliable scripts are developed, they can execute defined tests repeatedly with less direct human effort.
5. **Important limitation:** Automation still needs people to design, review, maintain and investigate results. It does not eliminate human resources entirely.

Therefore, automation can reduce repetitive manual effort, especially for stable regression suites, but it is not automatically cheaper for every test.

## (b) Write a short note on Reviews.
A **review** is a static testing activity in which people examine a work product—such as requirements, design documents, test cases or source code—to identify defects and improvements **without executing the software**.

### Objectives
- Detect defects early.
- Check correctness, completeness, consistency and clarity.
- Verify compliance with requirements and standards.
- Share knowledge and improve work-product quality.
- Reduce the cost of fixing defects later.

### Common review types
1. **Informal review:** A simple peer check without a formal process.
2. **Walkthrough:** The author guides participants through the work product and gathers feedback.
3. **Technical review:** Peers evaluate technical correctness and suitability.
4. **Inspection:** A formal, structured review with defined roles, preparation and recorded findings.

### Basic review process
```text
Planning
   |
   v
Preparation
   |
   v
Review Meeting / Examination
   |
   v
Record Defects
   |
   v
Rework and Follow-up
```

Reviews are useful because defects in requirements or design can be found before they become expensive coding or runtime problems.

---

# Q5. Answer the following questions (Any Two) — 5 marks each

## (a) Explain Software Testing Life Cycle (STLC) in detail.
**STLC** is a systematic sequence of testing activities performed to check whether software meets its requirements and quality expectations.

```text
Requirement Analysis
        |
        v
Test Planning
        |
        v
Test Case Design / Development
        |
        v
Test Environment Setup
        |
        v
Test Execution
        |
        v
Test Cycle Closure
```

### 1. Requirement Analysis
- Study functional and non-functional requirements.
- Identify testable requirements.
- Clarify ambiguities with stakeholders.
- Identify risks and required test data.

**Output:** Testable requirements and requirement understanding.

### 2. Test Planning
- Define scope and objectives.
- Choose the testing approach and test levels.
- Estimate effort, schedule and resources.
- Assign responsibilities and identify risks/tools.

**Output:** Test plan and estimates.

### 3. Test Case Design / Development
- Prepare test cases and test data.
- Cover positive, negative and boundary scenarios.
- Review test cases.
- Map test cases to requirements using RTM.

**Output:** Reviewed test cases, test data and traceability.

### 4. Test Environment Setup
- Prepare required hardware/software, configuration and access.
- Configure the application build and test data.
- Verify that the environment is ready.

**Output:** Ready test environment.

### 5. Test Execution
- Execute test cases.
- Compare actual and expected results.
- Record pass/fail status.
- Report defects and retest fixes.
- Perform regression testing when appropriate.

**Output:** Execution results and defect reports.

### 6. Test Cycle Closure
- Review test coverage and execution status.
- Summarize defects and unresolved risks.
- Prepare a test summary/closure report.
- Record lessons learned and closure status.

**Output:** Test summary report and closure information.

## (b) Explain White Box Testing with advantages and disadvantages.
**White-box testing** is a technique in which the tester uses knowledge of internal code, logic and structure to design tests. It is also known as structural or clear-box testing.

### What it checks
- Statements and executable lines.
- Branches and decision outcomes.
- Conditions and program paths.
- Loops, functions and internal logic.

### Advantages
1. Finds internal logic defects, such as incorrect conditions and calculations.
2. Measures code coverage through statement and branch coverage.
3. Helps identify untested branches and paths.
4. Supports detailed testing of functions and modules.
5. Structural analysis may reveal unreachable or redundant code.

### Disadvantages
1. Requires programming knowledge.
2. Designing tests for complex paths can be time-consuming.
3. Tests may need updating when implementation changes.
4. May miss missing requirements or features that were never implemented.
5. High code coverage does not guarantee that all defects have been found.

## (c) Explain Acceptance Test-Driven Development (ATDD).
**Acceptance Test-Driven Development (ATDD)** is a development approach in which business stakeholders, developers and testers collaborate to define acceptance tests **before implementation**. These tests describe the conditions a feature must satisfy to be accepted.

### Process
```text
Discuss requirements with stakeholders
                 |
                 v
       Define acceptance criteria
                 |
                 v
       Write acceptance tests
                 |
                 v
          Develop the feature
                 |
                 v
       Execute acceptance tests
                 |
          +------+------+
          |             |
        Pass            Fail
          |             |
          v             v
      Accept feature   Fix and retest
```

### Benefits
- Builds a shared understanding of requirements.
- Clarifies acceptance criteria before development.
- Reduces ambiguity and misunderstandings.
- Provides clear checks for deciding whether a feature is complete.
- Encourages collaboration between business and technical team members.

**Example:** Before implementing ticket booking, the team agrees that successful payment must create a booking reference and display confirmation. This becomes an acceptance test.

---

# Q6. Answer the following questions (Any One) — 6 marks

## (a) Hospital Management System: patient name length must be 8 to 12 characters. Design Equivalence Partitioning test cases with at least 5 valid and 5 invalid cases.

**Requirement:** The registration counter clerk enters a patient's name. The accepted name length is **8 to 12 characters inclusive**.

**Equivalence Partitioning (EP)** divides possible inputs into classes expected to behave similarly. A representative value is selected from each class.

### Equivalence classes

| Class | Input length | Expected result |
|---|---|---|
| Invalid class 1 | Fewer than 8 characters | Reject |
| Valid class | 8–12 characters inclusive | Accept |
| Invalid class 2 | More than 12 characters | Reject |

### Test cases

| ID | Example name | Length | Class | Expected result |
|---|---|---:|---|---|
| EP01 | `Rameshka` | 8 | Valid — lower boundary | Accept |
| EP02 | `Pratiksha` | 9 | Valid | Accept |
| EP03 | `AakashJang` | 10 | Valid | Accept |
| EP04 | `Harshvardhan` | 12 | Valid — upper boundary | Accept |
| EP05 | `MaheshPat` | 9 | Valid | Accept |
| EP06 | `Aakash` | 6 | Invalid — too short | Reject |
| EP07 | `Ramesh` | 6 | Invalid — too short | Reject |
| EP08 | `Abcdefg` | 7 | Invalid — too short | Reject |
| EP09 | `HarshvardhanX` | 13 | Invalid — too long | Reject |
| EP10 | `abcdefghijklmn` | 14 | Invalid — too long | Reject |

*These examples test length only. If the system has separate rules for permitted characters, spaces or punctuation, those need additional equivalence classes.*

## (b) Write a manual test case for testing an entered e-mail address in any application.

### Test Case: Validate an entered e-mail address

| Field | Details |
|---|---|
| Test Case ID | EMAIL_VAL_001 |
| Test Case Title | Verify validation of an entered e-mail address |
| Objective | Check whether the application accepts a correctly formatted e-mail address and rejects an invalid format. |
| Preconditions | Application is open and the e-mail field is visible. |
| Valid Test Data | `student@example.com` |
| Invalid Test Data | `student.example.com` (missing `@`) |
| Steps | 1. Open the form. 2. Enter `student@example.com` in the e-mail field. 3. Submit. 4. Verify the result. 5. Repeat with `student.example.com`. |
| Expected Result | The valid address should pass format validation. The malformed address should be rejected with a suitable validation message; submission should be prevented if the field is required. |
| Actual Result | Fill during execution. |
| Status | Pass/Fail — fill after execution. |

### Additional e-mail validation cases

| ID | Input | Expected result |
|---|---|---|
| EMAIL_02 | `student@example.com` | Accept format |
| EMAIL_03 | `student.example.com` | Reject — missing `@` |
| EMAIL_04 | `student@` | Reject — incomplete address |
| EMAIL_05 | `@example.com` | Reject — missing local part |
| EMAIL_06 | Empty input | Required-field message if the field is mandatory |

---

## Exam Tips
- **2 marks:** Give a precise definition or list the requested points.
- **3 marks:** Define the concept and explain 4–6 relevant points.
- **4 marks:** Include a definition, key points and a short example or diagram.
- **5–6 marks:** Add a structured explanation, process/diagram and practical examples.
- For **BVA**, test values below, at and above each boundary.
- For **Equivalence Partitioning**, identify valid and invalid classes first.
- In a test case, include ID, preconditions, test data, steps and expected result.
