# Bug Reports List

| Information    |                          |
| -------------- | ------------------------ |
| **Group**      | `<!-- STQA_Group_03 -->` |
| **Created Date** | `<!-- 19/05/2026 -->`  |
| **System**     | https://stqa.rbc.vn      |
| **Reference**  | SRS v1.0                 |

---

## 1. BUG-REQ01-01: Incorrectly Rejecting a Valid Email

**Bug ID:** BUG-01 (Reference: TC-REQ07-01)

**Title:** The system displays the error message "Invalid Email" and refuses to add a new member when a correctly formatted email address is entered (e.g., binh.ly@email.com)

**Environment:**

- Browser: Chrome Version 125.0.0
- Operating System: Windows / macOS
- Application: Library Book Borrowing System (https://stqa.rbc.vn)

**Preconditions:**

- The user has successfully logged in with a **Librarian** account (`librarian@library.com`).
- The user is currently on the **Add New Member** screen.

**Steps to Reproduce:**

1. In the **Full Name** field, enter: `Lý Tân Binh`.
2. In the **Email** field, enter a valid email address containing a dot before the @ symbol: `binh.ly@email.com`.
3. In the **Phone Number** field, enter: `0988111222`.
4. Click the green **Add Member** button at the bottom of the form.

**Expected Result:**
The system accepts the data (because the email satisfies the SRS rules by containing an `@` symbol and a `.` in the domain part), proceeds to create the new member, and displays a success message.

**Actual Result:**
The system does not save the data and displays a red warning message stating `"Invalid Email."` directly above the Add Member button.

**Impact:**
The member creation process is incorrectly blocked for users with common valid email addresses (format: `[first-name].[last-name]@domain.com`). This causes frustration and disrupts the Librarian's work.

**Severity:**
**High** — A Validation Logic defect that breaks a core Member Management workflow. It directly prevents valid data from being entered into the system.

**Evidence:**

- Attached screenshot: <img width="2880" height="1704" alt="image" src="https://github.com/user-attachments/assets/a02adc22-5e26-4691-94ea-6b4fed411f35" /> _(Shows the input form and the red error message)._

**Suggested Fix:**
Review the email validation function (Regex Validation) in both the Frontend and Backend source code. The Regex pattern should be updated to allow the dot (`.`) character in the local part of the email address (before the `@` symbol). 

---

## 2. BUG-REQ02-01: Book Borrowing Status Is Not Updated Automatically in Real Time

**Bug ID:** BUG-02 (Reference: TC-02-04)

**Title:** The system does not automatically update book status in real time across different user sessions when a book borrowing action occurs

**Environment:**

- Browser: Chrome Version 125.0.0
- Operating System: Windows / macOS
- Application: Library Book Borrowing System (https://stqa.rbc.vn)

**Preconditions:**

- There are 2 valid accounts in the system: one Librarian account and one Member account.
- The book with ID `BOOK001` is initially in the "Available" status.

**Steps to Reproduce:**

1. Log in to the system simultaneously on 2 different devices/browsers: Session 1 uses the Librarian account (`librarian@library.com`), Session 2 uses the Member account (`dam.tran@email.com`).
2. In both sessions, navigate to the home page and locate book `BOOK001` (observe that the status label displays "Available" in both sessions).
3. In Session 2 (Member), click the borrow button for book `BOOK001`.
4. Return to the display screen of Session 1 (Librarian) and observe the status of book `BOOK001` without refreshing the page (F5).

**Expected Result:**
The system should instantly synchronize data in real time. The status of book `BOOK001` on the Librarian's screen should immediately change to the orange "Borrowed" status without requiring the user to manually refresh the page.

**Actual Result:**
The system does not automatically update data across sessions. On the Librarian's screen, book `BOOK001` still displays the old "Available" status. The status is only updated after pressing F5 to refresh the browser.

**Impact:**
Displayed data becomes inconsistent and unsynchronized among users working at the same time. This may lead to multiple Members attempting to borrow a book that is no longer available, causing data conflicts (Race Conditions) and reducing the overall UI/UX experience.

**Severity:**
**Medium** — A Real-time Synchronization logic defect. The core system functionality still works after refreshing the page, but the issue significantly affects the accuracy and reliability of the user interface.

**Evidence:**

- Attached screenshot: <img width="3840" height="2256" alt="image" src="https://github.com/user-attachments/assets/c2e6a5ef-c0f9-41f9-9bcb-9508bb120261" /> _(Shows two side-by-side screens: one has successfully borrowed the book, while the other still displays "Available")._

**Suggested Fix:**
Integrate and properly configure a real-time communication mechanism using WebSockets (e.g., Socket.io) or continuous data change listeners (Real-time Listeners/Subscriptions) on both the Frontend and Backend. The system should automatically emit status update events and push them to all active user sessions whenever a book's status changes.

---

## BUG-REQ03-01: The System Incorrectly Processes Queries When the Keyword Contains Leading or Trailing Spaces (Missing Trim Space Logic)

**Bug ID:** BUG-03 (Reference: TC-03-03)

**Title:** The system does not normalize input strings (Trim Space) before performing a search, resulting in incorrect search results

**Environment:**

* Browser: Chrome Version 125.0.0
* Operating System: Windows / macOS
* Application: Library Book Borrowing System (https://stqa.rbc.vn)

**Preconditions:**

* The user is logged in with a valid Member account.
* The system contains a book titled **"Basic Flutter Programming"**.
* The search bar works correctly for valid keywords.

**Steps to Reproduce:**

1. Log in to the system using a valid Member account.
2. Navigate to the system home page.
3. In the book search box, enter a keyword with leading and trailing spaces: `" Flutter "` (including one space before and after the word Flutter).
4. Press **Enter** or click the **Search** icon to perform the query.

**Expected Result:**

The system should automatically remove (trim) unnecessary leading and trailing spaces from the input string before performing the search. After normalizing the keyword to `"Flutter"`, the system should return the relevant result, which is the book **"Basic Flutter Programming"**.

**Actual Result:**

The system does not remove unnecessary spaces from the search keyword. Instead of performing the correct search query or displaying a "No Data Found" message, the system displays the entire default library book list, including unrelated books such as **"Data Structures"**, **"Computer Networks"**, etc.

**Impact:**

* Returns inaccurate search results, causing confusion for users.
* Reduces the usability of the search functionality.
* Indicates incomplete input handling and the absence of proper data normalization before querying.
* May affect user trust in the system when different input formats are used.

**Severity:**

**Medium** — Input Validation/Input Handling defect. It does not cause data loss but directly affects the accuracy of the search functionality.

**Evidence:**

* Attached screenshot: `<img width="3840" height="2256" alt="image" src="https://github.com/user-attachments/assets/8f657417-80d3-4532-a058-3c198600b08a" />`
* It can be observed that after searching with the keyword `" Flutter "`, the system displays the entire book list instead of results related to Flutter.

**Suggested Fix:**

* Normalize input data using the `trim()` function on the Frontend before sending the search request.
* Apply the `trim()` function on the Backend as well to ensure consistency and avoid relying entirely on Frontend validation.
* Add test cases covering the following scenarios:

  * Leading spaces in the input string.
  * Trailing spaces in the input string.
  * Both leading and trailing spaces.
  * Input strings containing only whitespace characters.
* Ensure that all search queries are executed against normalized input data.

---

## 4. BUG-REQ03-02: The Search Box Overrides and Completely Ignores the Book Category Filter

**Bug ID:** BUG-04 (Reference: TC-03-05)

**Title:** Logic conflict between the Search box and Category filter causes the system to ignore the category filtering condition when a keyword is entered (Search & Filter Conflict)

**Environment:**

- Browser: Chrome Version 125.0.0
- Operating System: Windows / macOS
- Application: Library Book Borrowing System (https://stqa.rbc.vn)

**Preconditions:**

- The user has successfully logged into the system.
- The user is on the home page displaying the book list and category filters.

**Steps to Reproduce:**

1. In the category filter toolbar, select the **"Economics"** category.
2. In the book search box above, enter the keyword of a book belonging to the Technology category: `"Flutter"`.
3. Execute the search and observe the displayed results list.

**Expected Result:**
The system should apply both filtering conditions simultaneously using `AND` logic (Category = Economics AND Keyword = Flutter). Since the Flutter book belongs to the Technology category rather than Economics, the system should return an empty result page and display the message "No books found."

**Actual Result:**
The system completely ignores the previously selected **"Economics"** filter and overrides it with the search result, displaying the book **"Basic Flutter Programming"** (which belongs to the Technology category) in the results list.

**Impact:**
This issue seriously violates the business logic of multi-criteria filtering. It effectively disables category-based filtering whenever a search keyword is entered, resulting in incorrect results and misleading information for users.

**Severity:**
**High** — Business Logic defect. It completely breaks the advanced search and filtering functionality defined in the system specification.

**Evidence:**

- Attached screenshot: <img width="3840" height="2256" alt="image" src="https://github.com/user-attachments/assets/392fc0a5-d6c9-4ea4-8bcb-c9f6c7e46b57" /> _(Shows the category dropdown set to "Economics" while the results display a Technology book.)_

**Suggested Fix:**
Update the query processing logic in the Backend or the filtering function in the Frontend. Ensure that data retrieval applies both conditions simultaneously by passing both parameters in the query:

`WHERE category = selected_category AND book_name LIKE %keyword%`

instead of allowing one filtering function to override the other.

---

## 5. BUG-REQ04-01: Members Can Borrow More Books Than the Allowed Limit (Maximum 3 Books)

**Bug ID:** BUG-05 (Reference: TC-04-04)

**Title:** The system does not enforce the maximum borrowing limit for Members, allowing the 4th and 5th books to be borrowed successfully without displaying any error message

**Environment:**

- Browser: Chrome (Latest Version)
- Operating System: Windows 11
- Application: Library Book Borrowing System (https://stqa.rbc.vn)

**Preconditions:**

- The system is in its initial data state.
- The Member account is active and in normal operating status.

**Steps to Reproduce:**

1. Access the system at https://stqa.rbc.vn and log in using the Member account: `dam.tran@email.com` / `password123`.
2. On the book list screen, click the **"Borrow Book"** button for any 3 books currently in the **"Available"** status (e.g., `BOOK001`, `BOOK002`, `BOOK003`).
3. Find a 4th book that is also in the **"Available"** status (e.g., `BOOK004`) and click the **"Borrow Book"** button.

**Expected Result:**
The system should verify the number of books currently borrowed by the Member account, block the borrowing action for the 4th book, and display a clear error message through a Dialog/Toast notification as specified in the SRS:

**"Maximum borrowing limit reached (3 books)."**

**Actual Result:**
The system does not check the borrowing limit and still allows a successful borrowing transaction for the 4th book (and continues to allow borrowing additional books). The 4th book immediately changes its status label to **"Borrowed"** as normal.

**Impact:**
This issue seriously violates a core library business rule defined in the SRS document. It may lead to book loss, resource management issues, and significant inaccuracies in operational statistics.

**Severity:**
**High** — Critical Business Logic defect. It breaks the most important control and validation mechanism of the book borrowing functionality.

**Evidence:**

- Attached screenshot: <img width="3840" height="2256" alt="image" src="https://github.com/user-attachments/assets/e5f4b4f7-d939-4a31-8e22-94d32a6393c6" /> _(Shows a borrowing history/list containing 4 or more borrowed books under the same account)._

**Suggested Fix:**
Add a validation check before approving a new borrowing transaction. Count the total number of active (not yet returned) borrowing records associated with the current user (`UserID`). If the result is greater than or equal to 3, immediately block the action and return an appropriate error response at both the Frontend and Backend API levels.

---

## 6. BUG-REQ05-01: Missing Confirmation Popup and Cancel Option When Returning a Book

**Bug ID:** BUG-06 (Reference: TC-05-05)

**Title:** The system immediately performs the book return action when the button is clicked without displaying a confirmation dialog (Popup/Modal Confirm) for user verification

**Environment:**

- Browser: Chrome Version 125.0.0
- Operating System: Windows / macOS
- Application: Library Book Borrowing System (https://stqa.rbc.vn)

**Preconditions:**

- The user has successfully logged into the system using a regular Member account.
- The user is on the **"My Borrowing Records"** page and currently has at least one borrowing record with the status **"Borrowed"**.

**Steps to Reproduce:**

1. Navigate to the **"My Borrowing Records"** management screen.
2. Locate any borrowing record currently displayed with the status **"Borrowed"**.
3. Click the **"Return Book"** button and observe the system's visual response.

**Expected Result:**
The system must display a warning Dialog/Modal asking the user to confirm the action with a clear message:

*"Are you sure you want to return this book?"*

The dialog should provide two options: **"Confirm"** and **"Cancel"**.

If the user clicks **"Cancel"**, the process must be completely aborted and the borrowing record status must remain unchanged.

**Actual Result:**
The system immediately processes the book return request and sends the API request to the server without any confirmation step, removing the user's ability to cancel the action in case of an accidental click.

**Impact:**
A significant User Experience (UX) issue. The absence of a confirmation mechanism for data-mutating actions increases the risk of accidental operations and may disrupt the normal borrowing workflow.

**Severity:**
**Medium** — UX/Interaction Design defect. The underlying business logic still functions correctly, but the system does not provide a safe and user-friendly interaction flow.

**Evidence:**

- Attached screenshot: <img width="3840" height="2256" alt="image" src="https://github.com/user-attachments/assets/8a8528ac-00ea-4d25-8065-cda70ce25533" /> _(Shows the borrowing record status changing immediately after clicking the button without any confirmation popup.)_

**Suggested Fix:**
Implement a Confirm Dialog/Modal component on the Frontend to intercept the click event. The API call to the Backend should only be triggered after the user explicitly clicks the **Confirm** button within the dialog.

---

## 7. BUG-REQ06-01: The "Overdue" Status Filter Works Incorrectly and Displays Invalid Data

**Bug ID:** BUG-07 (Reference: TC-06-03)

**Title:** The status filter uses incorrect logic and displays mixed results, including "Returned" borrowing records when the user selects the "Overdue" filter

**Environment:**

- Browser: Chrome Version 125.0.0
- Operating System: Windows / macOS
- Application: Library Book Borrowing System (https://stqa.rbc.vn)

**Preconditions:**

- The user has successfully logged in with the **Librarian** role (`librarian@library.com`).
- The system database contains both **Overdue** borrowing records and completed **Returned** records.

**Steps to Reproduce:**

1. Navigate to the **Borrowing Management** administration page.
2. Locate the status filter dropdown and select only the **"Overdue"** option.
3. Carefully review the status labels displayed for each record returned in the results table.

**Expected Result:**
When the **"Overdue"** status filter is applied, the system should return only borrowing records with the **"Overdue"** status. All records belonging to other statuses (**Borrowed**, **Returned**, etc.) must be completely excluded from the displayed results.

**Actual Result:**
The system returns a mixed and incorrect dataset, displaying both **"Overdue"** records and many completed records marked with the green **"Returned"** status.

**Impact:**
This defect significantly affects the accuracy of reporting and data management features. Librarians may be unable to accurately identify members with overdue books, making it difficult to send reminders and reducing overall library management efficiency.

**Severity:**
**High** — Business Logic & Data Query defect. The data filtering functionality is broken and returns an incorrect dataset that does not match the user's selected criteria.

**Evidence:**

- Attached screenshot: <img width="3840" height="2256" alt="image" src="https://github.com/user-attachments/assets/a8243258-9d0f-4664-a867-131a5e19046a" /> _(Shows the dropdown filter set to "Overdue" while the results table still contains multiple "Returned" records.)_

**Suggested Fix:**
Review the SQL query (or Backend filtering logic) responsible for retrieving borrowing records. Update the `WHERE` clause to ensure records are filtered using the correct status identifier (e.g., `WHERE status = 'OVERDUE'`). Also verify that no incorrect `OR` conditions or outdated data grouping logic are causing unrelated statuses to be included in the result set.

---

## 8. BUG-REQ07-01: Invalid Email Format Is Not Detected

**Bug ID:** BUG-08 (Reference: TC-REQ07-02)

**Title:** The system successfully creates a new member when an invalid email address is entered (missing a dot in the domain part)

**Environment:**

- Browser: Chrome Version 125.0.0
- Operating System: Windows / macOS
- Application: Library Book Borrowing System (https://stqa.rbc.vn)

**Preconditions:**

- The user has successfully logged in with a **Librarian** account (`librarian@library.com`).
- The user is currently on the **Add New Member** screen.

**Steps to Reproduce:**

1. In the **Full Name** field, enter: `Vũ Sai Lỗi`.
2. In the **Email** field, enter an email address without a dot (`.`) after the `@` symbol: `loi.vu@email`.
3. In the **Phone Number** field, enter: `0977333444`.
4. Click the **Add Member** button.

**Expected Result:**
The system should reject the new member creation request and display an error message asking the user to verify the email format.

(According to the SRS: *"The email address must contain a dot (.) in the domain part."*)

**Actual Result:**
The system fails to detect the invalid email format, accepts the data, and displays a success message indicating that the member has been added successfully.

**Impact:**
Invalid and improperly formatted data can be stored in the database. This violates basic data validation rules and may cause issues for future automated email services and integrations.

**Severity:**
**High** — Input Validation defect that directly impacts data integrity and data quality.

**Evidence:**

- Attached screenshot: <img width="2880" height="1704" alt="image" src="https://github.com/user-attachments/assets/b7646897-4028-4cbc-b910-4d067b610f11" /> _(Shows a successful creation message despite the invalid email address.)_

**Suggested Fix:**
Add or update the email validation Regex. The validation rule must require at least one dot (`.`) after the `@` symbol in the domain part (e.g., `@domain.com`).

---


