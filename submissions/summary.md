# Test Summary — Test Summary Report

> This is a Quality Assurance activity aimed at evaluating the overall quality of the Library Management system based on test results, business requirement compliance, and the impact level of the detected defects.

---

## 1. Team Information

| Item                  | Information                |
| --------------------- | -------------------------- |
| **Team**              | STQA-03                    |
| **Class**             | STQA                       |
| **Report Date**       | 23/05/2026                 |
| **System Under Test** | https://stqa.rbc.vn — v1.0 |

---

## 2. Results Overview

| Metric                     | Value   |
| -------------------------- | ------- |
| Total Test Cases           | 39      |
| Pass                       | 29      |
| Fail                       | 8       |
| Blocked                    | 2       |
| Not Run                    | 0       |
| **Pass Rate**              | 74.35%  |
| **Number of Detected Bugs**| 8       |

### Distribution by Functional Group

| Functional Group               | TC | Pass | Fail | Bug | Evaluation        |
| ------------------------------ | -- | ---- | ---- | --- | ----------------- |
| REQ-01: Login                  | 5  | 5    | 0    | 0   | Good              |
| REQ-02: View Book List         | 4  | 3    | 1    | 1   | Fairly Good       |
| REQ-03: Search & Filter Books  | 6  | 4    | 2    | 2   | Needs Improvement |
| REQ-04: Borrow Books           | 5  | 4    | 1    | 1   | Needs Improvement |
| REQ-05: Return Books           | 5  | 3    | 1    | 1   | Average           |
| REQ-06: Overdue Processing     | 5  | 3    | 1    | 1   | Average           |
| REQ-07: Member Management      | 4  | 2    | 2    | 2   | Poor              |
| REQ-08: Look up Borrowing Slips| 5  | 5    | 0    | 0   | Good              |

### Bug Distribution by Severity

| Severity | Quantity | Bug IDs                                                          |
| -------- | -------- | ---------------------------------------------------------------- |
| High     | 5        | BUG-REQ01-01, BUG-REQ03-02, BUG-REQ04-01, BUG-REQ06-01, BUG-REQ07-01 |
| Medium   | 3        | BUG-REQ02-01, BUG-REQ03-01, BUG-REQ05-01                         |
| Low      | 0        | None                                                             |

---

## 3. Test Design Techniques Used

| Technique                               | Applied to Which REQ?          | Number of TCs Used | Application Explanation                                                                                                                                                        |
| --------------------------------------- | ------------------------------ | ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Equivalence Partitioning (EP)**       | REQ-01, REQ-07, REQ-08         | 10                 | Divides input data into valid and invalid classes (existing/non-existing email, correct/incorrect email format, duplicate/unique email, valid/invalid account).                |
| **Boundary Value Analysis (BVA)**       | REQ-01, REQ-04                 | 2                  | Tests boundary values such as the maximum limit of 3 borrowed books or empty data fields.                                                                                      |
| **Decision Table Testing**              | REQ-04                         | 5                  | Tests combinations of business conditions when borrowing books: member status, book status, and the limit of currently borrowed books.                                         |
| **State Transition Testing**            | REQ-05, REQ-06, REQ-08         | 6                  | Tests state changes of books and borrowing slips (Borrowing → Returned → Overdue) as well as account statuses within business workflows.                                       |
| **Role-Based Testing (Authorization)**  | REQ-02, REQ-06, REQ-07, REQ-08 | 8                  | Tests access control and functionalities of each role (Librarian and Member), including feature visibility and blocking unauthorized access.                                  |
| **Negative Testing**                    | REQ-01, REQ-04, REQ-05, REQ-08 | 8                  | Tests system responses to invalid data or unauthorized actions, such as incorrect logins, invalid book borrowing, and cross-privilege access.                                  |
| **Happy Path Testing**                  | REQ-02, REQ-03, REQ-05, REQ-06 | 9                  | Tests successful business workflows when users perform correct actions with valid input data.                                                                                  |
| **UI / UX Testing**                     | REQ-02, REQ-05, REQ-06, REQ-08 | 6                  | Tests UI display, data structure, functional buttons, color coding/statuses, and user experience.                                                                              |
| **Filter / Search Testing**             | REQ-03                         | 6                  | Tests search and data filtering functionalities, string input processing, combining search criteria, and resetting filters.                                                    |
| **Real-time / Synchronization Testing** | REQ-02                         | 1                  | Tests data status synchronization capabilities across multiple user sessions without page reloads.                                                                             |

---

## 4. Software Quality Analysis

### 4.1. Strengths

* The **Login (REQ-01)** function operates stably with a **100%** Pass rate, accurately handling valid and invalid login scenarios.
* The **Look up Borrowing Slips (REQ-08)** function fully meets specification requirements with a **100%** Pass rate, ensuring role authorization and user data security.
* Core business processes such as **viewing book lists, borrowing books, and returning books** all perform well under normal usage scenarios.
* The **role authorization mechanism between Member and Librarian** is deployed relatively accurately, effectively restricting unauthorized access.
* The system interface is intuitive, with information clearly and consistently presented, facilitating easy user operations.

### 4.2. Weaknesses

* The **Member Management (REQ-07)** function contains critical defects in email format validation, both rejecting valid emails and accepting invalid ones.
* The **Search & Filter Books (REQ-03)** function handles incorrectly in certain scenarios, such as searching with extra whitespaces or combining multiple filtering conditions.
* The **Borrow Books (REQ-04)** function fails to properly apply borrowing quantity limit rules, allowing users to exceed the specified limits.
* The **Return Books (REQ-05)** function lacks a confirmation step prior to data updates, increasing the risk of accidental operations by users.
* The **Overdue Processing (REQ-06)** function still contains defects in data filtering, as it displays slips that do not belong to the overdue state.
* Certain test cases were **Blocked** due to data and test environment limitations, making it impossible to fully evaluate all business scenarios.
* With a Pass rate of **74.35%**, the system meets most functional requirements; however, business logic and data validation defects must be resolved prior to official deployment.

---

## 5. Bug Fixing Priority Proposals

> Priority criteria are determined based on the impact on the system's core business logic and the severity of the defect.

| Order | Bug          | Severity | Reason for Priority                                                                                  |
| ----- | ------------ | -------- | ---------------------------------------------------------------------------------------------------- |
| 1     | BUG-REQ04-01 | High     | Violates a critical business rule by allowing borrowing beyond the specified limits.                 |
| 2     | BUG-REQ07-01 | High     | Accepts incorrectly formatted emails, reducing data quality and impacting related functionalities.   |
| 3     | BUG-REQ06-01 | High     | The category filter uses an incorrect algorithm, mixed-displaying borrowing slips across multiple states. |
| 4     | BUG-REQ03-02 | High     | The search and filter logic operates incorrectly, returning inaccurate results to users.            |
| 5     | BUG-REQ06-01 | Medium   | The overdue filter displays incorrect data, affecting borrowing slip management capabilities.        |
| 6     | BUG-REQ03-01 | Medium   | Fails to handle redundant whitespaces in search keywords.                                            |
| 7     | BUG-REQ05-01 | Medium   | Lacks a confirmation mechanism prior to returning books, making accidental operations likely.        |
| 8     | BUG-REQ02-01 | Medium   | Book status does not synchronize instantaneously across working sessions.                            |

---

## 6. Conclusion

Through the execution of 39 test cases, the system achieved a 74.35% Pass rate, detecting a total of 8 defects with 2 cases Blocked due to a lack of test data.

The results indicate that the basic functions of the system operate relatively stably, particularly the Login and Borrowing Slip Lookup features. However, the system still suffers from multiple defects that directly impact core business flows such as book borrowing limits, member management, and data search processing.

Given the current High-severity defects, the team assesses that the system does not yet meet the criteria for official release. Priority must be given to fixing these critical defects, executing regression testing, and re-validating all related functionalities before deployment to the Production environment.

---

## 7. Lessons Learned

* Building the Input Domain Model (IDM) prior to Test Case design helps fully identify the data classes that need testing.
* Critical defects are usually concentrated in the business logic processing rather than the user interface.
* The quality of test data directly affects the ability to execute comprehensive test scenarios.
* Maintaining the traceability link among Requirements, Test Cases, Test Execution, and Bug Reports enhances traceability and quality management.

---

## 8. AI Usage Declaration

| AI Tool | Component Used For                                                 | How You Inspected/Edited It                                                |
| ------- | ------------------------------------------------------------------ | -------------------------------------------------------------------------- |
| ChatGPT | Supported reviewing Test Cases, Bug Reports, and building the Test Summary Report | The team inspected, edited, and re-verified the entire content before use. |
