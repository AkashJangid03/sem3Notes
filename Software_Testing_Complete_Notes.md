# SOFTWARE TESTING --- COMPLETE STUDY NOTES

**M.Sc. Computer Applications \| Units I--VI**

> **Source note:** These notes are organized from the six Software
> Testing lecture PDFs shared in this conversation. The lecture's topic
> order and terminology are retained where identifiable. Examples and
> explanatory wording are included to make the concepts easier to study;
> where the slides provide only a heading or a diagram, the notes do not
> claim to reproduce unseen details verbatim.

## Contents

1.  [Unit I --- Software Testing
    Fundamentals](#unit-i--software-testing-fundamentals)
2.  [Unit II --- Types of Testing](#unit-ii--types-of-testing)
3.  [Unit III --- Test Case
    Development](#unit-iii--test-case-development)
4.  [Unit IV --- Testing Techniques](#unit-iv--testing-techniques)
5.  [Unit V --- Testing Different
    Domains](#unit-v--testing-different-domains)
6.  [Unit VI --- Understanding Agile
    Testing](#unit-vi--understanding-agile-testing)
7.  [Quick Revision and Exam
    Questions](#quick-revision-and-exam-questions)

------------------------------------------------------------------------

# UNIT I --- SOFTWARE TESTING FUNDAMENTALS

## 1. Basic System Concepts

  -----------------------------------------------------------------------
  Term                    Meaning                 Example
  ----------------------- ----------------------- -----------------------
  **System**              An orderly group of     Hospital Management
                          people or components    System
                          working together to     
                          achieve a specific      
                          goal.                   

  **Subsystem**           A smaller working       In-patient department
                          component/module within (IPD)
                          a larger system.        

  **Boundary**            The limits that define  Functions included in a
                          what is inside and      hospital application
                          outside a system.       

  **Environment**         External elements that  Patients, suppliers,
                          affect or interact with regulations
                          a system.               

  **Feedback**            Information or          User feedback or a test
                          suggestions used to     report
                          evaluate or improve a   
                          system.                 

  **Organization**        People coordinated to   Hospital staff and
                          achieve a specific      departments
                          goal.                   
  -----------------------------------------------------------------------

## 2. System Structure and Functional Decomposition

A large system is divided into smaller subsystems and functions. This
helps identify modules, responsibilities, menus and testing scope.

### Example: Hospital Management System

``` text
                    HOSPITAL MANAGEMENT SYSTEM
                               |
             +-----------------+------------------+
             |                 |                  |
            IPD               OPD              CASUALTY
             |                 |                  |
     +-------+-------+   +-----+-------+   +------+--------+
     |       |       |   |             |   |      |        |
  Admission Ward  Records Registration Medicine Accident Emergency
     |               |                  |        |
  Bed/room        Patient/doctor       Pharmacy Ambulance/police
  Medicine        information          records  records
  Pathology
  Operation
```

### Functional Decomposition Diagram (FDD)

An FDD breaks a system into its main functions, subfunctions and
lower-level operations.

**Steps to prepare an FDD:** 1. Write the system name at the top. 2.
Identify its major subsystems. 3. Break each subsystem into functions.
4. Add lower-level operations where useful. 5. Ensure the diagram
represents functional responsibilities rather than program execution
order.

### FDD example: Library Management System

``` text
                    LIBRARY MANAGEMENT
                            |
        +-------------------+------------------+
        |                   |                  |
   Book Management    Member Management    Circulation
        |                   |                  |
   Add/Search/Edit    Register/Edit/View   Issue/Return/Renew
        |                   |                  |
   Availability       Member status         Fine calculation
                            |
                       Reports
                            |
                    Overdue/Inventory
```

### FDD example: Online Purchase System

``` text
                     ONLINE PURCHASE
                            |
       +----------+----------+-----------+-----------+
       |          |          |           |           |
      User      Product     Cart       Payment      Orders
       |          |          |           |           |
    Register    Search     Add item    Pay         Track
    Login       Filter     Remove      Validate    Cancel
    Profile     Details    Quantity    Confirmation Returns
```

### FDD example: Movie Ticket Booking System

``` text
                    MOVIE TICKET BOOKING
                             |
      +----------+-----------+----------+-----------+
      |          |           |          |           |
     User      Movies      Showtimes   Seats       Booking
      |          |           |          |           |
    Login      Search      Select      Choose      Confirm
    Profile    Details     Theatre     Seat        Ticket
                             |          |           |
                           Date       Availability Payment
```

## 3. SDLC --- Software Development Life Cycle

**Definition:** SDLC is a conceptual framework describing activities in
a software development project from planning to maintenance. Different
SDLC models organize these activities in different ways.

### SDLC flow diagram

``` text
Planning / Feasibility
          |
          v
Requirements Analysis
          |
          v
System Design
          |
          v
Implementation / Coding
          |
          v
Testing
          |
          v
Deployment
          |
          v
Maintenance
```

  -----------------------------------------------------------------------
  Phase                   Main activities         Testing relevance
  ----------------------- ----------------------- -----------------------
  Planning                Define goals, scope,    Identify quality goals,
                          feasibility, resources  risks and test effort.
                          and constraints.        

  Requirements Analysis   Gather and document     Requirements should be
                          business/user needs.    clear, complete and
                                                  testable.

  Design                  Plan architecture,      Review designs and
                          modules, data and       prepare test approach.
                          interfaces.             

  Implementation          Develop code and        Developers perform
                          components.             component checks;
                                                  testers prepare test
                                                  cases.

  Testing                 Evaluate the integrated Find defects and report
                          software against        quality information.
                          requirements.           

  Deployment              Release software to     Perform appropriate
                          users.                  release/smoke checks.

  Maintenance             Fix defects and adapt   Retest fixes and run
                          software.               regression tests.
  -----------------------------------------------------------------------

The lecture slides note that SDLC helps pinpoint problems, set system
goals, determine boundaries and identify resource limitations.

## 4. Object-Oriented System Development Life Cycle

The Unit I slides include an object-oriented SDLC view. It links
actors/objects, object-oriented programming or construction, an
object-oriented language or CASE tool, and testing for user
satisfaction, usability and quality assurance.

``` text
Actors / Objects
       |
       v
Object-oriented analysis and design
       |
       v
Object-oriented programming / construction
       |
       v
Testing
  - User satisfaction
  - Usability
  - Quality assurance (QA)
```

## 5. Software Testing

**Definition:** Software testing is a continuous activity during
software development used to verify and validate the software/project
and measure its quality.

### Objectives of software testing

-   Find defects before they affect users.
-   Check whether requirements have been implemented.
-   Compare actual results with expected results.
-   Evaluate reliability, usability and other quality needs.
-   Provide evidence to help make release decisions.
-   Reduce the risk and cost of failures discovered after release.

### Verification vs Validation

  -----------------------------------------------------------------------
  Aspect                  Verification            Validation
  ----------------------- ----------------------- -----------------------
  Main question           Are we building the     Are we building the
                          product right?          right product?

  Focus                   Work products against   Software behaviour
                          specifications.         against user needs.

  Typical activities      Reviews, inspections,   Executing tests,
                          walkthroughs, static    acceptance tests and
                          analysis.               realistic scenarios.

  Code execution          Often does not require  Usually involves
                          executing the           executing the
                          application.            application.

  Example                 Review a login design   Try valid and invalid
                          against the             credentials on the
                          specification.          login page.
  -----------------------------------------------------------------------

## 6. STLC --- Software Testing Life Cycle

The slides describe STLC as a systematic, planned and sequential process
with six stages, from requirement analysis to test cycle closure.

``` text
1. Requirement Analysis
          |
          v
2. Test Planning
          |
          v
3. Test Case Design / Development
          |
          v
4. Test Environment Setup
          |
          v
5. Test Execution
          |
          v
6. Test Cycle Closure
```

  -----------------------------------------------------------------------
  Stage                               Main activities / outputs
  ----------------------------------- -----------------------------------
  Requirement Analysis                Understand requirements, identify
                                      testable requirements and clarify
                                      doubts.

  Test Planning                       Define scope, approach, resources,
                                      schedule, responsibilities, tools
                                      and risks.

  Test Case Design / Development      Create and review test cases, test
                                      data and requirement traceability.

  Test Environment Setup              Prepare hardware/software, access,
                                      configuration and test data; verify
                                      readiness.

  Test Execution                      Run test cases, record actual
                                      results, compare them with expected
                                      results and report defects.

  Test Cycle Closure                  Summarize coverage, defects,
                                      outcomes, lessons learned and
                                      closure status.
  -----------------------------------------------------------------------

**SDLC vs STLC:** SDLC covers the full software lifecycle; STLC focuses
specifically on the testing activities within a project.

------------------------------------------------------------------------

# UNIT II --- TYPES OF TESTING

## 1. Testing Classification

``` text
SOFTWARE TESTING
|
+-- By execution approach
|   +-- Manual Testing
|   +-- Automation Testing
|
+-- By knowledge of internals
|   +-- White-box Testing
|   +-- Black-box Testing
|   +-- Gray-box Testing
|
+-- By objective
|   +-- Functional Testing
|   +-- Non-functional Testing
|
+-- By test level
    +-- Unit Testing
    +-- Integration Testing
    +-- System Testing
    +-- Acceptance Testing
```

## 2. Manual Testing

**Definition:** Manual testing is performed by a tester who executes
test steps without using an automation script to perform the test
actions.

### Characteristics

-   The tester manually interacts with the application.
-   It can reveal visible and less obvious defects through human
    observation.
-   It considers the application from the end-user perspective.
-   It requires time and effort, particularly for repetitive tests.
-   The slides mention **Testpad** as a test-planning/checklist tool for
    writing and running test plans.

### Advantages

-   Useful for exploratory and ad-hoc testing.
-   Human judgement is useful for usability and visual checks.
-   Lower initial tooling cost.
-   Useful when a feature or interface changes frequently.

### Limitations

-   Repeated execution is time-consuming.
-   Results may vary between testers.
-   Large regression suites are difficult to run manually.

## 3. Automation Testing

**Definition:** Automation testing uses scripts and tools to execute
defined tests and report results.

### Characteristics

-   Requires suitable tools, scripts, test data and maintenance.
-   Can execute repetitive tests faster after initial setup.
-   Useful for regression testing and build verification.
-   The slides list **QTP/UFT** and **Selenium** as examples.

### Advantages

-   Consistent execution of repeated steps.
-   Faster repeated regression checks.
-   Useful for large data sets and frequent builds.
-   Can reduce repetitive manual effort.

### Limitations

-   Initial setup can be costly.
-   Scripts require maintenance when the application changes.
-   Automation only checks what the scripts and assertions specify.
-   Human judgement is still important for exploratory and usability
    testing.

### Manual vs Automation Testing

  -----------------------------------------------------------------------
  Criterion               Manual Testing          Automation Testing
  ----------------------- ----------------------- -----------------------
  Execution               Human performs steps.   Scripts/tools perform
                                                  defined steps.

  Speed                   Slower for repeated     Usually faster after
                          tests.                  setup.

  Initial cost            Lower tooling cost;     Higher setup/tooling
                          tester time is needed.  cost.

  Best suited for         Exploratory, usability  Repeated regression and
                          and one-off checks.     stable workflows.

  Repeatability           Can vary by tester.     Consistent when
                                                  scripts/environment are
                                                  stable.

  Human judgement         Strong for subjective   Limited to programmed
                          evaluation.             checks.

  Maintenance             Test cases and          Test cases, scripts and
                          documentation need      data need updating.
                          updating.               

  Limitation              Time-consuming at       Cannot judge every
                          scale.                  usability or
                                                  exploratory issue.
  -----------------------------------------------------------------------

## 4. White-box Testing

Also called **structural, glass-box, transparent-box or clear-box
testing** in the slides.

**Definition:** White-box testing designs tests using knowledge of
internal code structure and logic.

### What it checks

-   Statements and executable lines.
-   Conditions and branches.
-   Program paths and loops.
-   Functions, objects and internal logic.
-   Input handling inside code.

### Why use it?

-   Identify internal security holes.
-   Check the behaviour of conditions and loops.
-   Test functions, objects and statements individually.
-   Identify hidden logic errors and unnecessary code.

### Advantages

-   Helps identify structural and logic defects.
-   Can reveal untested branches and paths.
-   Supports code-level analysis and optimization.

### Limitations

-   Requires programming knowledge.
-   Test cases may need updates when implementation changes.
-   Passing structural tests does not prove that user requirements are
    correct.

## 5. Black-box Testing

**Definition:** Black-box testing checks externally visible behaviour
against requirements without relying on knowledge of the internal code.

### Main focus

-   Inputs and outputs.
-   Functional requirements.
-   User workflows.
-   Error messages and validation.
-   Expected and unexpected input.

**Example:** Enter valid and invalid login credentials and verify the
result.

## 6. Gray-box Testing

**Definition:** Gray-box testing combines external behavioural testing
with partial knowledge of internal design, architecture or data
handling.

**Example:** Test a registration form while also knowing how its data is
stored in the database.

### White-box vs Black-box vs Gray-box

  -------------------------------------------------------------------------
  Type              Internal          Main basis          Example
                    knowledge                             
  ----------------- ----------------- ------------------- -----------------
  White-box         Detailed          Statements,         Exercise both
                    code/logic        conditions,         outcomes of an
                    knowledge         branches, paths     `if` statement.

  Black-box         Not required      Requirements,       Test
                                      inputs and outputs  valid/invalid
                                                          login details.

  Gray-box          Partial knowledge External behaviour  Test form
                                      plus                submission and
                                      architecture/data   verify database
                                      knowledge           effects.
  -------------------------------------------------------------------------

## 7. Functional Testing

Functional testing checks **what the system does** against functional
requirements.

Examples: - Login and logout. - Search and filtering. - Adding an item
to a cart. - Payment and order confirmation. - Report generation.

## 8. Non-functional Testing

Non-functional testing checks **how well the system operates** against
quality attributes and operating constraints.

The slides give this distinction: - **Functional:** Does login
succeed? - **Non-functional:** How many users can log in at the same
time?

  -----------------------------------------------------------------------
  Type                    Purpose                 Example
  ----------------------- ----------------------- -----------------------
  Performance Testing     Check responsiveness    Measure response time
                          and resource use.       during a specified
                                                  workload.

  Load Testing            Check behaviour under   Simulate expected
                          expected/specified      concurrent users.
                          load.                   

  Stress Testing          Observe behaviour       Increase load beyond
                          beyond normal operating the expected peak.
                          limits.                 

  Stability Testing       Check whether the       Run a long-duration
                          system remains stable   test.
                          over time.              

  Usability Testing       Assess ease of learning Check navigation,
                          and use.                labels and form
                                                  clarity.

  Compatibility Testing   Check across browsers,  Test supported
                          devices, OSs or         browsers.
                          configurations.         
  -----------------------------------------------------------------------

## 9. Test Levels

``` text
Unit Testing
     |
     v
Integration Testing
     |
     v
System Testing
     |
     v
Acceptance Testing
```

### Unit Testing

Tests an individual function, class or module.

-   Example: test a function that calculates a discount.
-   Helps locate defects close to the code.

### Integration Testing

Tests interactions between connected modules.

-   Example: check that checkout correctly communicates with the payment
    and order services.
-   Focuses on interfaces, data exchange and dependencies.

### System Testing

Tests the complete integrated application against requirements.

-   Example: test a complete purchase from login through order
    confirmation.
-   Includes functional and applicable non-functional requirements.

**Advantages noted in the slides:** clarifies expected application
behaviour, tests from the user perspective, helps find defects before
production and can improve efficiency.

**Limitations noted in the slides:** redundant testing can occur and
logical errors may still be missed.

### Acceptance Testing

Checks whether the system meets user/business acceptance needs.

-   Example: a business user confirms that the order workflow satisfies
    the agreed requirements.

------------------------------------------------------------------------

# UNIT III --- TEST CASE DEVELOPMENT

## 1. Test Case

**Definition:** A test case is a documented set of conditions, input
data, preconditions, execution steps and expected results used to verify
a particular scenario or requirement.

A test case provides a starting point for test execution.

## 2. Test Documentation

Test documentation consists of artifacts prepared before or during
testing. It helps estimate testing effort, measure coverage, track
resources and monitor execution progress.

### Types of testing documents

  -----------------------------------------------------------------------
  Document                            Meaning / purpose
  ----------------------------------- -----------------------------------
  **Test Policy**                     High-level document describing
                                      organizational testing principles,
                                      methods and important testing
                                      goals.

  **Test Strategy**                   High-level document identifying the
                                      testing approach and test levels
                                      for a project.

  **RTM --- Requirement Traceability  Connects requirements to test cases
  Matrix**                            to help track coverage.

  **Defect Report**                   Records a flaw that causes the
                                      system to fail to perform as
                                      expected.

  **Test Case**                       Documents preconditions, input
                                      values, steps, expected output,
                                      postconditions and result for a
                                      scenario.
  -----------------------------------------------------------------------

### Advantages of test documentation

-   Reduces ambiguity while allocating testing tasks.
-   Provides a systematic approach to testing.
-   Can be used as training material for new testers.
-   Helps plan quality work within a time limit.
-   Supports setup through configuration documents and operator manuals.
-   Improves transparency with clients and stakeholders.

### Disadvantages of test documentation

-   Can be costly and time-consuming.
-   Poorly trained authors may not know what to document.
-   Updating documents can be tiring.
-   Poor documentation may reflect badly on the product even when the
    product works well.

## 3. Components of a Test Case

  -----------------------------------------------------------------------
  Field                               Description
  ----------------------------------- -----------------------------------
  Test Case ID                        Unique identifier,
                                      e.g. `LOGIN_001`.

  Title/Description                   Short statement of the scenario.

  Preconditions                       Conditions that must be true before
                                      execution.

  Test Steps                          Ordered actions performed by the
                                      tester.

  Test Data                           Values used in the test.

  Expected Result                     Correct behaviour specified by the
                                      requirement.

  Actual Result                       What happened during execution.

  Status                              Pass, Fail, Blocked or Not Run,
                                      according to team convention.

  Postcondition                       Expected state after execution.

  Notes/Defect ID                     Additional observations or linked
                                      defect reference.
  -----------------------------------------------------------------------

## 4. Example: Login Test Cases

  -----------------------------------------------------------------------
  ID                Scenario / test   Steps (summary)   Expected result
                    data                                
  ----------------- ----------------- ----------------- -----------------
  LOGIN_001         Valid username    Open login; enter User reaches the
                    and password      valid             expected account
                                      credentials;      page.
                                      submit.           

  LOGIN_002         Valid username,   Enter valid       Access is denied
                    wrong password    username and      and a suitable
                                      incorrect         error is shown.
                                      password; submit. 

  LOGIN_003         Empty required    Leave fields      Required-field
                    fields            empty; submit.    validation
                                                        appears; login
                                                        does not proceed.

  LOGIN_004         Invalid email     Enter malformed   Format validation
                    format            email and submit. appears if email
                                                        format is
                                                        required.

  LOGIN_005         Password masking  Type a password.  Password is
                                                        obscured
                                                        according to
                                                        requirements.

  LOGIN_006         Logout then       Log in, log out,  Protected content
                    revisit protected then revisit      is not accessible
                    page              protected URL.    without a valid
                                                        session.
  -----------------------------------------------------------------------

### Execution record template

  -------------------------------------------------------------------------------------------
  Test Case   Test Step     Test Data           Expected   Actual      Status      Notes
  ID                                            Output     Result                  
  ----------- ------------- ------------------- ---------- ----------- ----------- ----------
  LOGIN_001   Submit valid  Valid               Account    Fill during Pass/Fail   Defect ID
              credentials   username/password   page opens execution               if failed

  LOGIN_002   Submit        Valid               Access     Fill during Pass/Fail   Defect ID
              incorrect     username/wrong      denied     execution               if failed
              password      password                                               
  -------------------------------------------------------------------------------------------

**Important:** Expected results should be specific enough to decide
whether a test passes or fails.

## 5. Preconditions and Postconditions

-   **Precondition:** A condition that must be true before a test
    starts.
-   **Postcondition:** The expected state after the test ends.

The slides use a real-life example of writing a letter: - Precondition:
a pen with a refill is available. - Postcondition: the letter has been
written and can be checked.

## 6. Test Analysis

The Unit III slides identify **SRS, BRS and FDD** as relevant documents
during test analysis.

### SRS --- Software Requirements Specification

The slides describe SRS as a document that: - Specifies how a software
system should be built. - Provides a roadmap to the people involved. -
Gives a high-level description of the software. - Includes functional
and non-functional specifications. - Describes external interfaces. -
Records constraints imposed on software design. - Provides a general
overview of the system.

### BRS --- Business Requirements Specification

The slides describe BRS as a formal document that: - Outlines high-level
business/functional requirements. - Records client requirements, written
and verbal. - Describes how trading partners perform roles, build
business relationships and share duties to interact efficiently.

### FDD --- Functional Design Document

The slides describe FDD as a document explaining how a process or
control system works.

The slides note that: - It explains how the planned system works and how
people interact with it. - It does not focus on high technical detail. -
It can be shared with team members, consumers and stakeholders for
feedback/review until agreed and signed. - Preparing it can be
time-consuming.

## 7. Writing Good Test Cases

1.  Understand the requirement and its acceptance criteria.
2.  Identify positive, negative and boundary scenarios.
3.  Define preconditions and test data.
4.  Write clear, ordered execution steps.
5.  Specify measurable expected results.
6.  Link the case to a requirement where possible.
7.  Review for ambiguity, duplication and missing coverage.
8.  Record actual results and defects during execution.

### Characteristics of a good test case

-   Clear and unambiguous.
-   Traceable to a requirement or risk.
-   Includes data, steps and expected results.
-   Repeatable.
-   Covers valid and invalid inputs where relevant.
-   Avoids unnecessary duplication.

------------------------------------------------------------------------

# UNIT IV --- TESTING TECHNIQUES

## 1. Meaning of Testing Techniques

Software testing techniques are methods used to test an application
against functional and non-functional requirements. Different techniques
are useful for finding different kinds of defects.

The slides describe testing as a **five-fold system**:

  Element              Meaning
  -------------------- ------------------------------
  Testers              Who performs testing?
  Coverage             What components are covered?
  Potential problems   Why is testing needed?
  Activities           How is testing performed?
  Evaluation           How are results compared?

## 2. Principles of Testing (as listed in the lecture slides)

1.  Tests should meet user requirements.
2.  Software testing can be performed by a third party.
3.  Exhaustive testing is not possible; testing should be risk-related.
4.  Planning should be done before testing.
5.  Start with small parts and extend toward larger parts.
6.  The Pareto rule (80/20 rule) suggests that many errors may be
    concentrated in a relatively small number of components. Treat this
    as a risk heuristic, not a guarantee.

## 3. Classification of Testing Techniques

``` text
SOFTWARE TESTING TECHNIQUES
|
+-- Static Testing
|   +-- Reviews
|   +-- Static Analysis
|       +-- Control Flow
|       +-- Data Flow
|
+-- Dynamic Testing
    |
    +-- Structure-based
    |   +-- Statement Coverage
    |   +-- Decision/Branch Coverage
    |   +-- Condition Coverage
    |   +-- Multiple-condition Coverage
    |
    +-- Experience-based
    |   +-- Error Guessing
    |   +-- Exploratory Testing
    |
    +-- Specification-based
        +-- Equivalence Partitioning
        +-- Boundary Value Analysis
        +-- Decision Tables
        +-- State Transition Testing
        +-- Use Case Testing
```

## 4. Static Testing

Static testing finds potential defects **without executing the
program**.

### Benefits

-   Can find issues early in development.
-   May reduce the cost of fixing defects.
-   Can improve product quality.
-   Often costs less than finding the same issue after execution or
    release.

### Reviews

Reviews involve people examining requirements, designs or other
documents and identifying discrepancies.

### Static Analysis

Static analysis identifies potential defects in code without executing
the program.

-   **Control-flow analysis:** focuses on calling structure, functions,
    methods and flow.
-   **Data-flow analysis:** focuses on how data objects are defined,
    used and passed.

## 5. Dynamic Testing

Dynamic testing finds defects by **executing the program** with selected
inputs and observing behaviour.

-   Checks actual behaviour against expected results.
-   Includes positive and negative test scenarios.
-   Requires execution environments and test data.
-   Can take more time and resources than some static checks.

## 6. Structure-based Testing and Coverage

  -----------------------------------------------------------------------
  Coverage type           Meaning                 Simple example
  ----------------------- ----------------------- -----------------------
  **Statement Coverage**  Checks whether each     Execute each line at
                          executable statement    least once.
                          has run.                

  **Decision/Branch       Checks whether each     Test both true and
  Coverage**              decision outcome has    false outcomes of an
                          been taken.             `if`.

  **Condition Coverage**  Checks whether each     For `A AND B`, ensure A
                          Boolean subcondition    and B each take both
                          has evaluated to true   values.
                          and false.              

  **Multiple-condition    Tests combinations of   For two conditions,
  Coverage**              Boolean subconditions.  consider TT, TF, FT and
                                                  FF where feasible.
  -----------------------------------------------------------------------

Coverage is a measurement of what has been exercised; it does **not**
guarantee that all defects have been found.

## 7. Equivalence Partitioning

**Definition:** Equivalence Partitioning divides the input domain into
classes expected to behave similarly. A representative value is selected
from each class instead of testing every possible value.

### Example: age allowed from 18 through 60

  Partition                   Range             Representative value
  --------------------------- --------------- ----------------------
  Invalid --- below minimum   age \< 18                           17
  Valid                       18 ≤ age ≤ 60                       35
  Invalid --- above maximum   age \> 60                           61

## 8. Boundary Value Analysis (BVA)

**Definition:** Boundary Value Analysis concentrates on values at and
near the edges of an allowed range, where errors are commonly found.

For the inclusive range **18--60**:

  Boundary case          Value
  -------------------- -------
  Just below minimum        17
  Minimum                   18
  Just above minimum        19
  Just below maximum        59
  Maximum                   60
  Just above maximum        61

### Equivalence Partitioning vs BVA

  -----------------------------------------------------------------------
  Equivalence Partitioning            Boundary Value Analysis
  ----------------------------------- -----------------------------------
  Divides input into                  Focuses on the edges of ranges.
  expected-behaviour classes.         

  Selects representative values from  Selects boundary and near-boundary
  classes.                            values.

  Example: one valid age and invalid  Example: 17, 18, 19, 59, 60, 61.
  ages below/above.                   
  -----------------------------------------------------------------------

## 9. Decision Table-Based Testing

A decision table shows combinations of conditions and the corresponding
actions. It is useful when a business rule depends on multiple
conditions.

### Example: login decision table

  ------------------------------------------------------------------------------
  Condition/action   Rule 1         Rule 2         Rule 3         Rule 4
  ------------------ -------------- -------------- -------------- --------------
  Username valid?    Yes            Yes            No             No

  Password valid?    Yes            No             Yes            No

  Expected action    Allow login    Reject login   Reject login   Reject login
  ------------------------------------------------------------------------------

Each meaningful rule combination can become a test case.

## 10. State Transition Testing

**Definition:** State transition testing checks how a system changes
state after events or inputs. It is useful when the response depends on
the current state.

### Example: login account

``` text
ACTIVE ACCOUNT
  | correct password
  +--------------------> AUTHENTICATED
  |
  | wrong password repeatedly
  +--------------------> LOCKED
                           |
                           | login attempt
                           +-------------> ACCESS DENIED
```

Possible scenarios include successful login, failed login, repeated
failures, locked-account access and recovery/unlock behaviour if
specified.

## 11. Use Case Testing

Use case testing derives scenarios from a user's goal and the end-to-end
interactions needed to achieve it.

### Example: online purchase

-   **Main flow:** search product → add to cart → checkout → pay →
    receive confirmation.
-   **Alternate flow:** payment is declined; the order must not be
    marked paid.
-   **Exception flow:** network fails during payment; the application
    should handle the failure safely and avoid duplicate processing.

## 12. Experience-based Testing

### Error Guessing

The tester uses experience to predict likely defects.

Examples: - Empty required field. - Invalid email format. - Very long
input. - Repeated click on Submit. - Network interruption. - Invalid or
expired session.

### Exploratory Testing

The tester learns the application, designs tests and executes them
iteratively, adapting based on observations.

------------------------------------------------------------------------

# UNIT V --- TESTING DIFFERENT DOMAINS

## 1. Web Domain Testing

The slides note that web applications may use HTML, CSS and JavaScript.
Websites may be static or dynamic, and may be single-page, multi-page or
progressive web applications.

The lecture identifies these testing levels for web applications: - Unit
testing --- e.g. JavaScript/Python components. - Integration testing ---
modules and their interactions. - System testing --- the full
application. - Acceptance testing. - Performance testing.

The slides list browsers such as Chrome, Safari, Edge, Firefox, Internet
Explorer, Opera and Edge Legacy as examples of browsers to test. The
actual list should follow the application's supported-browser
requirements. The slides also mention MS Excel for test-case design.

### Web Testing Definition

Web testing checks a website/web application for potential bugs before
it is made live and accessible to the public. It checks functionality,
usability, security, compatibility, performance, traffic handling and
site functionality.

### Web testing activities

  -----------------------------------------------------------------------
  Area                                Checks from the lecture topic
  ----------------------------------- -----------------------------------
  Functionality                       Interface, APIs, database,
                                      security, client/server behaviour.

  Link testing                        Internal links, outgoing links,
                                      actor links and mail-to links.

  HTML/CSS                            Syntax errors, readable colour
                                      scheme and standards compliance.

  Form testing                        Form scripts, default values,
                                      database interaction and form
                                      formatting.

  Business workflows                  End-to-end workflow through pages;
                                      negative scenarios.

  Usability                           Menus, buttons, links, content
                                      spelling/grammar and alternative
                                      text for images.

  Interface testing                   Requests and outputs; appropriate
                                      handling of errors; internal errors
                                      should not be exposed to end users.

  Performance                         Traffic handling and request
                                      processing.
  -----------------------------------------------------------------------

The slides list QTP, IBM Rational and Selenium as examples of tools, and
mention usability tools such as Chalkmark, Clicktale, Clixpy and
Feedback Army.

## 2. Finance / Banking Application Domain Testing

The lecture identifies three major banking testing processes: 1.
Functionality 2. Performance 3. Security

### Main purpose

-   Banking software should run smoothly without errors.
-   It should remain protected.
-   Financial transactions and balances should be correct.

### Banking functions mentioned in the slides

-   Transfer money.
-   Deposit money.
-   Withdraw money.
-   Balance enquiry.
-   Fixed deposits.

### Why domain knowledge matters

-   Reduces training time.
-   Helps with quick defect tracking.
-   Improves understanding of UI features and backend processing.
-   Builds familiarity with workflows, business processes and rules.
-   Helps testers understand technical terminology.

### Banking test examples

  -----------------------------------------------------------------------
  Scenario                            What to verify
  ----------------------------------- -----------------------------------
  Money transfer                      Correct source/destination, amount
                                      and transaction result.

  Deposit/withdrawal                  Balance and transaction record are
                                      updated correctly.

  Balance enquiry                     Displayed balance matches the
                                      recorded account state.

  Invalid transaction                 System rejects the transaction
                                      according to the business rule.

  Security                            Authentication, authorization and
                                      protection of sensitive data.

  Retry/failure                       Transaction handling remains
                                      consistent after an interruption.
  -----------------------------------------------------------------------

The last table gives practical examples to apply the lecture's
functional, performance and security categories.

## 3. E-commerce Domain Testing

**Definition:** E-commerce testing evaluates an online store to ensure
reliability, functionality and security, and to check conformity with
client requirements.

The slides identify objectives including software reliability, software
quality, system assurance and optimum performance. Tools listed include
UsabilityHub, HotJar, Feng-GUI, Optimizely and FiveSecondTest.

### Types of testing for e-commerce systems

  -----------------------------------------------------------------------
  Type                                Checks/processes identified in the
                                      slides
  ----------------------------------- -----------------------------------
  Functionality                       Develop test cases from business
                                      requirements; execute tests;
                                      analyze results and report defects.

  Usability                           Check non-intuitive design, poor
                                      navigation, lack of help/support
                                      and catalogue navigation; test with
                                      real users; gather feedback and
                                      improve.

  Security                            Perform vulnerability assessments;
                                      implement security
                                      patches/measures; update security
                                      protocols.

  Session Management                  Check session expiration and
                                      session storage.

  Backup and Recovery                 Check failure/failover recovery,
                                      backup failure and fault tolerance.

  Transactions                        Check transaction integrity,
                                      throughput and auditing.

  Shopping / Order Processing /       Check shopping cart, order
  Purchasing                          processing, payment processing and
                                      order tracking.

  Internationalization                Check language support and display,
                                      cultural sensitivity and regional
                                      accounting.
  -----------------------------------------------------------------------

### Practical e-commerce scenarios

-   Add an item to the cart and change its quantity.
-   Verify the order total and applicable discounts.
-   Check successful and declined payments.
-   Check that an unsuccessful payment does not create a paid order.
-   Verify order tracking.
-   Test session expiry.
-   Check recovery behaviour after a service interruption.
-   Verify language and regional display where supported.

## 4. Healthcare Domain Testing

The slides describe healthcare testing as testing applications for
standards, safety, compliance and cross-dependencies with other
entities.

### Objectives shown in the slides

-   Software reliability.
-   Software quality.
-   System safety.
-   Optimum performance.
-   Software efficiency.

The slides show interactions among patients/consumers, hospitals,
healthcare and life-science solution vendors, insurance companies and
regulatory authorities. They display the terms **HIPPA, OASIS and
HCFA1500**; retain the lecture's spelling when studying the slide.

### Types of testing for healthcare systems

  -----------------------------------------------------------------------
  System                              Testing processes shown in the
                                      slides
  ----------------------------------- -----------------------------------
  Provider System                     Write test cases for
                                      doctors/hospitals; add/update
                                      doctor/hospital information; login;
                                      claim status; invalid login
                                      credentials.

  Broker System (insurance agent)     Add/update broker information;
                                      insurance agency/agent; cashless
                                      and cash-return services.

  Patient System                      Add/edit/view patient; generate
                                      premium bill and payments;
                                      registration; maintain
                                      dependent/family information.

  Claim System                        Identify cashless/cash-return
                                      claim; handle claims (the slides
                                      mention Rajiv Gandhi Yojana);
                                      validate invalid procedure and
                                      diagnostic codes.
  -----------------------------------------------------------------------

### Healthcare testing considerations

-   Check that the correct records can be added, updated and viewed.
-   Test login and invalid credentials.
-   Verify claim status and claim handling.
-   Check procedure and diagnostic code validation.
-   Verify that interactions between patient, provider, broker and claim
    systems behave as specified.

## 5. Insurance Domain Testing

The Unit V outline explicitly includes Insurance Domain Testing. The
available slide text also places insurance companies in the
healthcare-system ecosystem and mentions broker/insurance-agent,
cashless/cash-return and claim workflows.

Based on those lecture details, revise: - Broker and insurance-agent
information. - Policy/customer-related data flows represented in the
course materials. - Cashless and cash-return claim paths. - Claim status
and claim processing. - Validation of related codes and records where
the system requires them.

**Source limitation:** The available extracted slide text for this topic
overlaps with healthcare content and does not clearly establish a
complete independent list of insurance-testing categories. Do not treat
the list above as a verbatim or exhaustive source list.

## 6. Telecom Domain Testing

The Unit V outline includes Telecom Domain Testing. In the extracted
text available for the uploaded slides, a complete detailed list of
telecom test types was not visible. Use the lecture PDF itself for any
exact instructor-provided telecom checklist.

For general understanding only, telecom applications commonly involve
customer/service workflows, plan changes, usage records, billing and
service availability. These examples are explanatory, not a claim that
each item appeared in the provided slides.

## 7. Domain Comparison

  -----------------------------------------------------------------------
  Domain                              Topics explicitly visible in the
                                      lecture material
  ----------------------------------- -----------------------------------
  Web                                 Functionality, links, HTML/CSS,
                                      forms, business workflow,
                                      usability, interface and
                                      performance.

  Banking                             Functionality, performance,
                                      security; transfer, deposit,
                                      withdrawal, balance enquiry and
                                      fixed deposits.

  E-commerce                          Functionality, usability, security,
                                      session management,
                                      backup/recovery, transactions,
                                      purchasing and
                                      internationalization.

  Healthcare                          Reliability, quality, safety,
                                      performance/efficiency; provider,
                                      broker, patient and claim systems.

  Insurance                           Insurance domain listed;
                                      healthcare-related slides include
                                      broker/agent, cashless/cash-return
                                      and claims.

  Telecom                             Domain listed in the unit outline;
                                      detailed extracted checklist not
                                      established here.
  -----------------------------------------------------------------------

------------------------------------------------------------------------

# UNIT VI --- UNDERSTANDING AGILE TESTING

## 1. Introduction to Agile

The slides describe Agile as flexible, adaptable, iterative and focused
on frequent inspection and customer satisfaction. Changes in
requirements are welcomed and considered during development.

The lecture mentions methods including Rational Unified Process, Scrum,
Crystal Clear, Extreme Programming, Adaptive Software Development,
Feature Driven Development and Dynamic Systems Development Method
(DSDM). The slides state that these became collectively referred to as
Agile methodologies after the Agile Manifesto was published in 2001.

## 2. Agile Process Model

Agile divides work into smaller iterations. Each iteration includes
activities across the software development lifecycle before a working
product is demonstrated to the client. The slides describe iterations
commonly lasting one to four weeks.

``` text
Product backlog / requirements
             |
             v
      Iteration planning
             |
             v
  Requirements analysis
             |
             v
           Design
             |
             v
        Build / code
             |
             v
           Testing
             |
             v
   Demonstration / feedback
             |
             v
 Updated backlog → next iteration
```

### Main characteristics

-   Work is divided into smaller iterations.
-   Each iteration includes planning, analysis, design, development and
    testing.
-   Working software is demonstrated to the client.
-   Feedback helps adapt the next iteration.
-   Smaller increments can reduce risk and delivery time.
-   Agile still requires planning; the plan is revisited as the project
    evolves.

## 3. Scrum

The slides describe Scrum as an Agile development process focused on
managing work in team-based development.

  -----------------------------------------------------------------------
  Role                                Responsibility in the lecture
                                      slides
  ----------------------------------- -----------------------------------
  **Scrum Master**                    Facilitates the process, organizes
                                      meetings and helps remove
                                      obstacles.

  **Product Owner**                   Creates/prioritizes the product
                                      backlog and helps decide
                                      functionality for iterations.

  **Scrum Team**                      Organizes its work to complete the
                                      sprint/cycle.
  -----------------------------------------------------------------------

Scrum helps organizations adjust to changing requirements and evolving
business goals.

## 4. Agile Testing Strategy

-   Testing is integrated throughout each iteration.
-   Testers collaborate with developers, product owners and
    stakeholders.
-   Requirements and acceptance criteria guide test design.
-   Frequent feedback helps expose defects earlier.
-   Regression checks help protect existing behaviour.
-   Demonstrations and feedback can change priorities for later
    iterations.

## 5. Traditional Sequential Approach vs Agile

  --------------------------------------------------------------------------
  Aspect                  Traditional sequential  Agile approach
                          approach (general       
                          comparison)             
  ----------------------- ----------------------- --------------------------
  Planning                More planning and scope Planning is repeated and
                          definition upfront.     refined per iteration.

  Testing timing          Testing may be          Testing occurs throughout
                          concentrated after      each iteration.
                          implementation.         

  Requirements            Changes may involve     Changes are considered and
                          formal change control.  prioritized as work
                                                  evolves.

  Feedback                Often arrives at        Frequent feedback from
                          milestones or phases.   working increments.

  Delivery                Often a larger release  Smaller incremental
                          after multiple phases.  releases/demonstrations.

  Risk                    Defects may be found    Earlier feedback can
                          late if feedback is     expose issues sooner.
                          delayed.                
  --------------------------------------------------------------------------

This is a general comparison for study; actual processes vary by
organization.

## 6. Test-Driven Development (TDD)

**Definition:** Test-Driven Development is a practice in which a test is
written before the implementation that makes it pass.

### TDD cycle

``` text
RED: Write a failing test
          |
          v
GREEN: Write the simplest code that passes
          |
          v
REFACTOR: Improve the code while tests stay green
          |
          +--------------------> Repeat
```

-   **Red:** the new test fails because the required behaviour is not
    implemented.
-   **Green:** implement enough code to pass the test.
-   **Refactor:** improve code design/readability without changing
    expected behaviour.

**Benefits:** quick feedback, clearer expected behaviour and tests that
can support regression checks.

## 7. Behaviour-Driven Development (BDD)

BDD describes expected behaviour in language shared by business
stakeholders, testers and developers. Scenarios commonly use
**Given--When--Then**.

  -----------------------------------------------------------------------
  Part                    Meaning                 Example
  ----------------------- ----------------------- -----------------------
  Given                   Initial                 Given a registered user
                          context/precondition    is on the login page

  When                    Action/event            When the user enters
                                                  valid credentials and
                                                  submits

  Then                    Expected observable     Then the user reaches
                          result                  the account page
  -----------------------------------------------------------------------

BDD emphasizes shared understanding of observable behaviour.

## 8. Acceptance Test-Driven Development (ATDD)

ATDD involves stakeholders collaborating before development to define
acceptance tests that describe what the feature must do to be accepted.

  -----------------------------------------------------------------------
  TDD                     BDD                     ATDD
  ----------------------- ----------------------- -----------------------
  Write a test before     Describe expected       Agree acceptance tests
  implementation.         behaviour in shared     with stakeholders
                          scenarios.              before implementation.

  Often focuses on        Focuses on observable   Focuses on business
  development-level       behaviour.              acceptance criteria.
  behaviour.                                      

  Tests guide coding and  Scenarios improve       Tests align the team on
  refactoring.            shared understanding.   what "accepted" means.
  -----------------------------------------------------------------------

## 9. Benefits of Agile Testing

-   Earlier feedback and defect discovery.
-   Better alignment with business/user expectations.
-   Adaptability to changing requirements.
-   Frequent regression checks.
-   Visible progress through working increments.
-   Shorter feedback loops and earlier risk discovery.

## 10. Agile Estimation Techniques

The lecture outline explicitly includes common Agile estimation
techniques. The following are commonly used examples for understanding;
confirm the exact list expected by the instructor against the slides.

  -----------------------------------------------------------------------
  Technique                           Description
  ----------------------------------- -----------------------------------
  Planning Poker                      Team members estimate
                                      independently, reveal estimates and
                                      discuss differences.

  Story Points                        Relative estimate of complexity,
                                      effort and uncertainty; not a
                                      direct number of hours.

  T-shirt Sizing                      Rough categories such as XS, S, M,
                                      L and XL.

  Affinity Estimation                 Group backlog items by relative
                                      size, then refine.

  Ideal Time                          Estimate focused work time under
                                      ideal conditions, not elapsed
                                      calendar time.
  -----------------------------------------------------------------------

## 11. Defect Management Process

Defect management records, prioritizes, tracks and resolves defects
found during testing. Status names can differ between organizations.

``` text
New / Logged
     |
     v
Triaged: severity, priority and ownership
     |
     v
Assigned → In Progress
     |
     v
Fixed / Resolved
     |
     v
Retest
  /     \
Pass    Fail
 |       |
 v       v
Closed  Reopened / returned to development
```

### Common defect report fields

  -----------------------------------------------------------------------
  Field                               Purpose
  ----------------------------------- -----------------------------------
  Defect ID                           Unique identifier.

  Summary/Description                 Concise title and reproduction
                                      details.

  Steps to reproduce                  Exact sequence that reveals the
                                      defect.

  Expected vs actual result           Shows the difference between
                                      required and observed behaviour.

  Environment/build                   Where the defect was found.

  Severity                            Impact of the defect on system
                                      operation.

  Priority                            Urgency/order for fixing it.

  Status/Owner                        Current stage and responsible
                                      person.
  -----------------------------------------------------------------------

### Severity vs Priority

-   **Severity:** how seriously the defect affects the system.
-   **Priority:** how urgently the team should fix it.

They are related but not identical.

## 12. Agile Testing Metrics and Reporting

  -----------------------------------------------------------------------
  Metric                  What it indicates       Caution
  ----------------------- ----------------------- -----------------------
  Test execution progress Tests passed, failed,   A high pass rate alone
                          blocked or not run.     does not prove good
                                                  coverage.

  Defect count/trend      Defects over time or by Interpret with severity
                          build.                  and test scope.

  Defect leakage          Defects found after a   Depends on consistent
                          stage/release that were recording.
                          not found earlier.      

  Test coverage           Requirements, risks or  Coverage does not
                          code areas exercised by guarantee absence of
                          tests.                  defects.

  Defect cycle time       Time from logging to    Consider defect
                          resolution/closure.     complexity and
                                                  severity.

  Automation pass rate    Outcomes of automated   Flaky tests/environment
                          checks.                 failures can distort
                                                  results.
  -----------------------------------------------------------------------

### Reporting principles

-   Report progress and risks clearly.
-   Include blocked and unexecuted tests, not only pass/fail counts.
-   Track defect severity and status.
-   Interpret metrics together rather than using one number as a quality
    verdict.

------------------------------------------------------------------------

# QUICK REVISION AND EXAM QUESTIONS

## 1. Important Definitions

  -----------------------------------------------------------------------
  Term                                Short definition
  ----------------------------------- -----------------------------------
  Software Testing                    Evaluating software to find defects
                                      and check requirements/quality.

  Verification                        Checking work products against
                                      specifications.

  Validation                          Checking whether the product meets
                                      user needs.

  SDLC                                Lifecycle of software development
                                      from planning to maintenance.

  STLC                                Structured lifecycle of testing
                                      activities.

  Test Case                           Documented conditions, data, steps
                                      and expected outcome for a
                                      scenario.

  RTM                                 Matrix linking requirements to test
                                      cases.

  White-box Testing                   Testing internal structure or
                                      logic.

  Black-box Testing                   Testing external behaviour against
                                      requirements.

  Static Testing                      Examining artifacts without
                                      executing the program.

  Dynamic Testing                     Testing by executing the program.

  Equivalence Partitioning            Dividing inputs into classes
                                      expected to behave similarly.

  Boundary Value Analysis             Testing values at and around input
                                      boundaries.

  Regression Testing                  Re-running relevant tests after
                                      changes to check existing
                                      behaviour.

  TDD                                 Write a test, make it pass, then
                                      refactor.

  BDD                                 Specify expected behaviour in
                                      shared, scenario-based language.

  ATDD                                Define acceptance tests
                                      collaboratively before
                                      implementation.
  -----------------------------------------------------------------------

## 2. Common Comparison Questions

1.  Verification vs Validation.
2.  SDLC vs STLC.
3.  Manual Testing vs Automation Testing.
4.  White-box vs Black-box vs Gray-box Testing.
5.  Functional vs Non-functional Testing.
6.  Unit vs Integration vs System vs Acceptance Testing.
7.  Static vs Dynamic Testing.
8.  Equivalence Partitioning vs Boundary Value Analysis.
9.  TDD vs BDD vs ATDD.
10. Severity vs Priority.

## 3. Likely Long-answer / Diagram Questions

1.  Define software testing and explain its purpose.
2.  Explain system, subsystem, boundary, environment and feedback.
3.  Draw an FDD for Library Management, Online Purchase or Movie Ticket
    Booking.
4.  Explain SDLC phases and the role of testing in each.
5.  Explain STLC and draw its six stages.
6.  Compare manual and automation testing with examples.
7.  Explain white-box, black-box and gray-box testing.
8.  Explain functional and non-functional testing.
9.  Explain unit, integration, system and acceptance testing.
10. Define test case and test documentation; explain document types,
    advantages and disadvantages.
11. Write test cases for a login page with positive and negative
    scenarios.
12. Explain SRS, BRS and FDD as described in the lecture.
13. Explain static and dynamic testing, including coverage types.
14. Explain equivalence partitioning and BVA with a numerical example.
15. Explain decision table, state transition and use case testing.
16. Explain web application testing activities.
17. Explain banking testing processes: functionality, performance and
    security.
18. Explain e-commerce testing categories.
19. Explain healthcare provider, broker, patient and claim systems.
20. Explain Agile methodology and draw the iterative process.
21. Explain TDD, BDD and ATDD with examples.
22. Explain defect management and Agile testing metrics.

## 4. Exam Checklist

-   Can you define key terms in 2--3 precise sentences?
-   Can you redraw SDLC, STLC, testing classification and Agile
    diagrams?
-   Can you create a comparison table with several criteria?
-   Can you write a test case with preconditions, steps, data and
    expected results?
-   Can you solve an equivalence partitioning/BVA example?
-   Can you explain the source-specific domain testing tables?
-   Can you distinguish what the lecture explicitly states from
    additional examples?
