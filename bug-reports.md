---

# BUG-10

## Bug ID
BUG-10

## Title
Book status does not synchronize in real-time between active sessions

## Environment
- Browser: Chrome v136.0
- Operating System: Windows 11
- Application: ABC Library Management System
- URL: https://stqa.rbc.vn

## Preconditions
- User A and User B are logged in simultaneously on different devices/browsers.

## Steps to Reproduce
1. User A and User B view the homepage simultaneously.
2. User B clicks to borrow `BOOK001`.
3. Observe the screen of User A without refreshing.

## Expected Result
The status of `BOOK001` on User A's screen should immediately update to "Borrowed" (Đang mượn).

## Actual Result
The status remains "Available" (Có sẵn) on User A's screen until manual refresh (F5).

## Severity
**Medium**

## Related Test Case
TC-04 — Verify real-time status update on borrow action

## Suggested Fix
Implement WebSocket or Server-Sent Events (SSE) to broadcast status changes to active clients.

---

# BUG-11

## Bug ID
BUG-11

## Title
Search fails when keyword contains leading or trailing spaces (No Trim logic)

## Environment
- Browser: Chrome v136.0
- Operating System: Windows 11
- Application: ABC Library Management System
- URL: https://stqa.rbc.vn

## Preconditions
- The book "Lập trình Flutter cơ bản" exists in the database.

## Steps to Reproduce
1. Navigate to the search bar.
2. Enter the keyword with spaces: `" Flutter "` (space before and after).
3. Press Enter.

## Expected Result
The system should automatically trim the spaces and return the book "Lập trình Flutter cơ bản".

## Actual Result
The system fails to trim the string, treats the spaces as part of the exact keyword, and displays "Không tìm thấy sách".

## Severity
**Medium**

## Related Test Case
TC-07 — Search book with leading and trailing spaces

## Suggested Fix
Call the `.trim()` method on the search input string in the frontend or backend before executing the database query.

---

# BUG-12

## Bug ID
BUG-12

## Title
Search query overrides and ignores active Category Filter logic

## Environment
- Browser: Chrome v136.0
- Operating System: Windows 11
- Application: ABC Library Management System
- URL: https://stqa.rbc.vn

## Preconditions
- Sách "Flutter" thuộc thể loại "Công nghệ".

## Steps to Reproduce
1. Click the Category dropdown and select "Kinh tế".
2. Type `Flutter` into the search bar.
3. Observe the results.

## Expected Result
The list should be empty ("Không tìm thấy sách") because "Flutter" does not belong to the "Kinh tế" category. Both Search and Filter logic should apply simultaneously (AND logic).

## Actual Result
The system completely ignores the "Kinh tế" category filter and displays the "Flutter" book from the "Công nghệ" category.

## Severity
**High**

## Related Test Case
TC-09 — Filter and Search conflict handling

## Suggested Fix
Update the API logic to combine search and filter using `AND` operators in the SQL query: `WHERE category_id = X AND (title LIKE '%Y%' OR author LIKE '%Y%')`.