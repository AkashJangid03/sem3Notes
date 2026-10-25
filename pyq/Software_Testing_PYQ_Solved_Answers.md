# Software Testing — Solved Question Paper
**M.Sc. Computer Applications — Semester III**  
**CSA603: Software Testing | NEP 2020 Pattern**

Answers are organized according to the uploaded two-page question paper. All visible questions are answered for practice.

---

# Q1. Answer the following questions (Any Six) — 2 marks each

## (a) Define Software Testing.
Software testing is the process of evaluating software to identify defects and verify that it meets specified requirements. It compares actual results with expected results and provides information about software quality.

## (b) “Sometimes regression testing is the best candidate for automation.” True/False? Justify.
**True.** Regression testing checks whether existing functionality still works after code changes, bug fixes or enhancements. The same tests may need to be repeated after every build, so automation reduces execution time, improves repeatability and provides faster feedback. Exploratory and usability testing may still require manual testing.

## (c) Quote two examples of non-functional testing.
1. **Performance testing:** Checks response time, speed and behaviour under workload.
2. **Usability testing:** Checks how easily users can understand and use the application.
Other examples include load, stress, stability and compatibility testing.

## (d) List the five folds of Testing Techniques.
The five folds listed in the course material are:
1. **Testers** — Who performs testing?
2. **Coverage** — What is covered?
3. **Potential problems** — Why is testing performed?
4. **Activities** — How is testing performed?
5. **Evaluation** — How are actual results compared with expected results?

## (e) Define Intruder.
An **intruder** is an unauthorized person or entity that attempts to access a computer system, network or data without permission. An intruder may try to view, modify, steal or disrupt protected information or services.

## (f) List basic steps for creating RTM.
**RTM (Requirement Traceability Matrix)** maps requirements to test cases to help verify coverage.
1. List all requirements and assign each a unique Requirement ID.
2. Identify test conditions and prepare test cases for each requirement.
3. Record links between Requirement IDs and Test Case IDs in a matrix.
4. Review for requirements without test cases and test cases without requirement links.
5. Update the RTM when requirements or test cases change.

## (g) Write the pre-condition of Online Ticket Booking System.
Possible preconditions for a booking test case:
- The ticket-booking website/app is available.
- The user is logged in, if login is required for the scenario.
- The required journey/event, date and time are available.
- Seats/tickets are available.
- Valid payment details are available if checkout is being tested.

*Preconditions depend on the scenario. A search test may not require login or payment details.*

---

# Q2. Answer the following questions (Any Four) — 3 marks each

## (a) Explain the advantages of Performance Testing.
Performance testing evaluates an application's responsiveness, stability, scalability and resource use under a specified workload.

1. **Measures speed and response time:** Shows whether the application responds within acceptable limits.
2. **Identifies bottlenecks:** Helps find slow database queries, inefficient code, network delays or resource constraints.
3. **Checks stability:** Reveals failures or degradation during sustained use.
4. **Evaluates scalability:** Indicates behaviour as users, transactions or data volume increase.
5. **Improves user experience:** Reduces delays and interruptions.
6. **Supports capacity planning:** Helps estimate infrastructure and resource needs.
7. **Reduces production risk:** Finds performance problems before release.

## (b) Explain disadvantages of Test Documentation in detail.
1. **Time-consuming:** Preparing detailed test plans, cases and reports requires time.
2. **Costly:** Writing, reviewing and maintaining documentation adds project cost.
3. **Requires skilled people:** Authors must understand the system and know what information is useful.
4. **Maintenance effort:** When requirements or software change, related documents and test cases may need updates.
5. **Outdated information:** If documents are not maintained, testers may follow incorrect steps or expected results.
6. **Over-documentation:** Excessive detail can consume time that could otherwise be used for testing.
7. **Poor documentation can mislead:** Ambiguous or incomplete documents can cause inconsistent execution and incorrect conclusions.

## (c) What is Use Case Testing? Explain in short.
**Use Case Testing** derives test scenarios from the ways an actor/user interacts with a system to achieve a goal. It checks the main flow and relevant alternative or exception flows.

**Example — Online ticket booking:**
- Main flow: choose event/journey → select date/time → choose seat → pay → receive confirmation.
- Alternative flow: selected seat is no longer available.
- Exception flow: payment fails or the network disconnects.

It helps test end-to-end user workflows from the user's perspective.

## (d) Write a note on Banking Domain.
Banking domain testing checks whether banking software works correctly, securely and reliably. The course material identifies three major testing processes:

1. **Functionality testing:** Verifies money transfer, deposit, withdrawal, balance enquiry and fixed deposits.
2. **Performance testing:** Checks response time and behaviour under expected or peak workloads.
3. **Security testing:** Checks authentication, authorization and protection of accounts and financial data.

**Importance of domain knowledge:** It reduces training time, helps with quick defect tracking, improves understanding of UI features and backend processing, and helps testers understand workflows, business rules and technical terminology.

## (e) Discuss Agile Testing Benefits in detail.
Agile testing is integrated throughout iterative development rather than being postponed until the end.

1. **Early defect detection:** Frequent testing identifies defects sooner.
2. **Fast feedback:** Testers, developers and stakeholders can discuss issues during each iteration.
3. **Adaptability:** Testing responds to changing requirements and priorities.
4. **Better collaboration:** Team members share acceptance criteria and test results.
5. **Continuous regression testing:** Repeated checks protect existing functionality as features are added.
6. **Frequent delivery:** Each iteration can produce a working increment for demonstration or release.
7. **Reduced risk:** Smaller increments and short feedback loops can expose problems earlier.
8. **Customer alignment:** Feedback from demonstrations helps ensure the product meets user needs.

---

# Q3. Answer the following questions (Any Three) — 4 marks each

## (a) Write a note on Defect/Bug Life Cycle in detail.
The **Defect Life Cycle** is the sequence of states a defect passes through from reporting until it is closed or otherwise resolved. Exact status names vary by organization.

```text
New / Logged
     |
     v
Triaged / Reviewed
     |
     v
Assigned
     |
     v
Open / In Progress
     |
     v
Fixed / Resolved
     |
     v
Retesting
   /     \\
Pass     Fail
 |        |
 v        v
Closed   Reopened
            |
            v
       Assigned again
```

**Stages:**
1. **New/Logged:** Tester records the defect with description, reproduction steps, expected result and actual result.
2. **Triaged/Reviewed:** Team evaluates validity, severity, priority and scope.
3. **Assigned:** Defect is allocated to a responsible developer/team member.
4. **Open/In Progress:** The defect is investigated and corrected.
5. **Fixed/Resolved:** Developer records that a correction has been made.
6. **Retesting:** Tester repeats the relevant test on the updated build.
7. **Closed:** Tester confirms the issue is fixed and closes it.
8. **Reopened:** If the defect remains or reappears, it is returned for further work.

Some teams also use statuses such as **Rejected/Invalid**, **Duplicate**, **Deferred** or **Cannot Reproduce**.

## (b) Apply Boundary Value Analysis for voter age 18 to 115. Find nominal value. Write 5 valid and invalid test cases.
The valid age range is **18 to 115 inclusive**.

For Boundary Value Analysis (BVA), test values at and around both boundaries:
- Lower boundary: 17, **18**, 19
- Upper boundary: 114, **115**, 116

The **nominal value** is a typical value well inside the valid range. One suitable nominal value is **30**.

| Test Case | Age input | Category | Expected result |
|---|---:|---|---|
| TC01 | 18 | Valid — lower boundary | Accepted |
| TC02 | 19 | Valid — just above lower boundary | Accepted |
| TC03 | 30 | Valid — nominal value | Accepted |
| TC04 | 114 | Valid — just below upper boundary | Accepted |
| TC05 | 115 | Valid — upper boundary | Accepted |
| TC06 | 17 | Invalid — below lower boundary | Rejected |
| TC07 | 16 | Invalid — below lower boundary | Rejected |
| TC08 | 116 | Invalid — above upper boundary | Rejected |
| TC09 | 117 | Invalid — above upper boundary | Rejected |
| TC10 | 0 | Invalid — outside range | Rejected |

**Conclusion:** Ages from 18 through 115 should be accepted; values below 18 or above 115 should be rejected. This gives five valid and five invalid test cases.

## (c) Predict the challenges in Healthcare Domain.
Healthcare software has complex workflows and handles sensitive patient information. Common testing challenges include:

1. **Data privacy and security:** Patient records must be protected from unauthorized access.
2. **Regulatory and standards compliance:** Systems may need to comply with applicable healthcare standards and regulations.
3. **Data accuracy and integrity:** Incorrect patient, diagnosis, procedure, prescription or claim data can have serious consequences.
4. **Integration complexity:** Systems exchange information among hospitals, doctors, patients, insurance companies, laboratories and regulatory entities.
5. **Patient safety and reliability:** Critical workflows must behave consistently and safely.
6. **Complex business rules:** Claims, billing, eligibility and cashless/cash-return processes may involve many conditions.
7. **Interoperability:** Different systems may use different formats, codes and interfaces.
8. **Performance and availability:** Important services must remain responsive and accessible.

The course slides specifically emphasize standards, safety, compliance, cross-dependencies, reliability, quality, system safety, optimum performance and efficiency.

## (d) Write a note on Acceptance Test-Driven Development (ATDD).
**Acceptance Test-Driven Development (ATDD)** is a development approach in which business stakeholders, developers and testers collaborate to define acceptance tests **before implementation**. These tests describe the conditions a feature must satisfy to be accepted.

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

**Benefits:**
- Builds a shared understanding of requirements.
- Clarifies acceptance criteria before development.
- Reduces ambiguity and misunderstandings.
- Provides clear checks for deciding whether a feature is complete.
- Encourages collaboration between business and technical team members.

**Example:** Before implementing ticket booking, the team agrees that successful payment must create a booking reference and display a confirmation. This becomes an acceptance test.

---

# Q4. Answer the following questions (Any Two) — 4 marks each

## (a) Explain Automation Testing Process in detail.
Automation testing uses tools and scripts to execute repeatable tests and compare actual results with expected results.

```text
1. Requirement Analysis
          |
          v
2. Identify Automation Candidates
          |
          v
3. Select Tool and Define Strategy
          |
          v
4. Prepare Test Environment and Data
          |
          v
5. Design and Develop Test Scripts
          |
          v
6. Execute Automated Tests
          |
          v
7. Compare Results and Report Defects
          |
          v
8. Maintain Scripts and Run Regression Tests
```

**Steps:**
1. **Requirement analysis:** Understand features, requirements and expected behaviour.
2. **Identify automation candidates:** Select repeatable, stable and high-value tests such as regression tests.
3. **Tool selection:** Choose a tool based on application technology, skills, budget and compatibility.
4. **Environment/data setup:** Prepare the application build, accounts, test data and execution environment.
5. **Script development:** Write scripts and assertions for actions and expected outcomes.
6. **Execution:** Run scripts and capture results/logs.
7. **Result analysis:** Compare actual and expected results and report defects.
8. **Maintenance:** Update scripts when requirements, UI or workflows change; rerun appropriate regression tests.

Automation is not suitable for every test. Exploratory and subjective usability testing may still require manual testing.

## (b) Explain Dynamic Testing.
**Dynamic testing** is a technique in which software is executed with selected inputs and its actual behaviour is compared with expected behaviour.

```text
Select Test Cases
       |
       v
Prepare Test Data
       |
       v
Execute the Program
       |
       v
Observe Actual Results
       |
       v
Compare with Expected Results
       |
       v
Record Pass/Fail and Report Defects
```

**Characteristics:**
- Requires execution of the software.
- Tests actual runtime behaviour.
- Uses inputs and checks outputs or state changes.
- Can reveal failures that occur during execution.
- Includes positive, negative and boundary scenarios.

**Examples:** Enter valid/invalid login details; test ages at the range boundaries; divide by zero in a calculator; test successful and declined payments.

| Static Testing | Dynamic Testing |
|---|---|
| Does not execute the program. | Executes the program. |
| Reviews documents/code or uses static analysis. | Uses test inputs and observes actual behaviour. |
| Can find issues early in requirements/design/code. | Can reveal runtime failures and incorrect outputs. |
| Example: review requirements for ambiguity. | Example: execute a login test case. |

## (c) Write a note on Agile testing strategy.
An Agile testing strategy integrates testing into each iteration and encourages collaboration, quick feedback and continuous improvement.

1. **Early involvement:** Testers participate in requirement discussions and iteration planning.
2. **Acceptance criteria:** Requirements are expressed in clear, testable terms.
3. **Continuous testing:** Test cases are executed during the iteration, not only at the end.
4. **Automation where useful:** Stable, repeatable tests can be automated for fast feedback.
5. **Regression testing:** Existing functionality is rechecked after changes.
6. **Collaboration:** Testers, developers, product owners and stakeholders discuss risks and results.
7. **Defect prioritization:** Issues are assessed by impact, urgency and iteration goals.
8. **Feedback and adaptation:** Results and demonstrations help refine the backlog and next iteration.

```text
Planning → Analysis → Design → Development → Testing
   ^                                            |
   |                                            v
   +-------- Feedback / Retrospective ← Demonstration
```

Benefits include earlier defect discovery, adaptability, frequent feedback, better collaboration and improved alignment with user needs.

---

# Q5. Answer the following questions (Any Two) — 5 marks each

## (a) Explain Software Testing Life Cycle (STLC) in detail.
**STLC** is a systematic sequence of testing activities performed to ensure that software meets its requirements and quality expectations.

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
- Define testing scope and objectives.
- Choose testing approach and levels.
- Estimate effort, schedule and resources.
- Assign responsibilities and identify risks/tools.

**Output:** Test plan and estimates.

### 3. Test Case Design / Development
- Prepare test cases and test data.
- Cover positive, negative and boundary scenarios.
- Review test cases.
- Map test cases to requirements using RTM.

**Output:** Reviewed test cases, data and traceability.

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
- Prepare test summary/closure report.
- Record lessons learned and closure status.

**Output:** Test summary report and closure information.

## (b) Explain Black Box Testing with advantages and disadvantages.
**Black-box testing** checks software behaviour against requirements without requiring knowledge of the internal code structure.

```text
Test Input
    |
    v
+------------------+
|  Software System |
| (Internal logic  |
|   not inspected) |
+------------------+
    |
    v
Actual Output
    |
    v
Compare with Expected Output
```

**Example — Login screen:**
- Valid username + valid password → login should succeed.
- Valid username + wrong password → access should be denied.
- Empty required fields → validation message should appear.

### Advantages
1. Does not require knowledge of internal code.
2. Tests from the user/requirement perspective.
3. Helps identify missing or incorrect functionality.
4. Test cases can be designed from specifications.
5. Can be performed independently of implementation details.

### Disadvantages
1. Internal code paths may remain untested.
2. It can be difficult to identify the exact root cause of a failure.
3. Poor or incomplete requirements make test design difficult.
4. Some input combinations may be missed if coverage is limited.
5. It cannot by itself guarantee that internal logic is structurally correct.

## (c) Write a note on Behaviour-Driven Development (BDD).
**Behaviour-Driven Development (BDD)** describes how a system should behave using scenarios understandable to business stakeholders, testers and developers. It encourages agreement on expected behaviour and commonly uses **Given–When–Then**.

- **Given:** Initial context or preconditions.
- **When:** Action or event.
- **Then:** Expected observable outcome.

### Example: successful login
```text
Given the user has a registered account
And the user is on the login page
When the user enters valid credentials and submits
Then the user should reach the account page
```

### BDD process
1. Discuss required behaviour with stakeholders.
2. Identify examples and acceptance criteria.
3. Write clear scenarios using shared language.
4. Develop the feature to satisfy the scenarios.
5. Execute scenarios to check behaviour.
6. Update scenarios when requirements change.

### Benefits
- Improves communication between business and technical teams.
- Reduces ambiguity in requirements.
- Creates examples that can serve as acceptance checks.
- Focuses on observable behaviour rather than implementation details.
- Aligns development with user expectations.

---

# Q6. Answer the following questions (Any One) — 6 marks

## (a) Equivalence Partitioning for student name length 8 to 12 characters. Write at least 5 valid and invalid test cases.

**Requirement:** In the Admission System, the office clerk maintains a student's name. Name length must be from **8 to 12 characters inclusive**.

**Equivalence Partitioning (EP)** divides possible inputs into classes expected to behave similarly. A representative value from each class is selected for testing.

### Equivalence classes

| Class | Input length | Expected result |
|---|---|---|
| Invalid class 1 | Fewer than 8 characters | Reject |
| Valid class | 8 to 12 characters inclusive | Accept |
| Invalid class 2 | More than 12 characters | Reject |

### Test cases

| ID | Example name | Length | Class | Expected result |
|---|---|---:|---|---|
| EP01 | `Rameshka` | 8 | Valid — lower boundary | Accept |
| EP02 | `AakashJang` | 10 | Valid | Accept |
| EP03 | `Harshvardhan` | 12 | Valid — upper boundary | Accept |
| EP04 | `Pratiksha` | 9 | Valid | Accept |
| EP05 | `ShreyasPat` | 10 | Valid | Accept |
| EP06 | `Aakash` | 6 | Invalid — too short | Reject |
| EP07 | `Ramesh` | 6 | Invalid — too short | Reject |
| EP08 | `Abcdefg` | 7 | Invalid — too short | Reject |
| EP09 | `HarshvardhanX` | 13 | Invalid — too long | Reject |
| EP10 | `abcdefghijklmn` | 14 | Invalid — too long | Reject |

**Note:** These examples demonstrate length classes. If the system also restricts characters (e.g. letters only), those character rules need separate equivalence classes and test cases.

## (b) Write a manual test case for testing division by zero in Windows Calculator.

### Test Case: Division by Zero

| Field | Details |
|---|---|
| Test Case ID | CALC_DIV_ZERO_001 |
| Test Case Title | Verify calculator behaviour when dividing by zero |
| Objective | Check that Windows Calculator handles division by zero without crashing. |
| Preconditions | Windows Calculator is installed and can be opened. |
| Test Data | First number: `10`; operator: `/`; second number: `0` |
| Steps | 1. Open Windows Calculator. 2. Enter `10`. 3. Select division (`÷`). 4. Enter `0`. 5. Press `=`. |
| Expected Result | Calculator should not crash; it should show an appropriate error or undefined-result indication according to the version. |
| Actual Result | Fill during execution. |
| Status | Pass/Fail — fill after execution. |

### Additional manual test cases

| Test Case ID | Input / operation | Purpose | Expected result |
|---|---|---|---|
| CALC_DIV_ZERO_002 | `0 ÷ 0 =` | Check zero divided by zero. | No crash; appropriate undefined/error indication. |
| CALC_DIV_ZERO_003 | `-10 ÷ 0 =` | Check negative dividend. | No crash; appropriate error/undefined indication. |
| CALC_DIV_ZERO_004 | `10 ÷ 2 =` | Control test for normal division. | Result is `5`. |

*The precise wording/icon shown for division by zero can differ by Windows Calculator version. Record the actual result from the version being tested.*

---

## Final Exam Tips
- **2 marks:** Write a precise definition or list the requested points.
- **3–4 marks:** Define the concept, explain 4–6 points and add a small example/diagram.
- **5–6 marks:** Include a definition, process/diagram, detailed points and an example.
- In **BVA**, include values just below, at and just above each boundary.
- In **Equivalence Partitioning**, identify valid and invalid classes before choosing representatives.
- In test-case answers, include ID, input/test data, expected result and status wherever possible.
