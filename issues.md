
# Static Code Analysis Issue Log

**Project:** Support Ticket Tracker  
**File Analyzed:** `support_ticket_tracker.py`  
**Lab:** Lab 5 – Static Code Analysis

## Issues Identified and Fixes

| # | Issue | Type / Tool | Line(s) | Description | Fix Applied |
|---:|---|---|---|---|---|
| 1 | Unsafe `eval()` usage | Security – Bandit (B307) | Verify from before-report | `eval()` can execute arbitrary Python expressions when processing untrusted input. | Removed `eval()` and replaced it with safer handling. |
| 2 | Bare exception handling | Reliability – Bandit (B110, as recorded) | Verify from before-report | Broad exception handling can hide unexpected errors and make debugging difficult. | Replaced the exception-handling approach with explicit ticket-existence checks and clearer handling. |
| 3 | Mutable default argument | Correctness / Maintainability | Verify from original source | Using `audit_log=[]` as a default can cause the same mutable list to be reused across calls. | Changed the default to `None` and initialized the log within the function. |
| 4 | Missing ticket ID handling | Correctness | Verify from original source | Attempting to close a nonexistent ticket could raise a `KeyError`. | Added an explicit existence check and a not-found response. |
| 5 | Non-idiomatic method naming | Code Style | Verify from original source | `closeTicket()` did not follow the Python snake_case naming convention. | Renamed `closeTicket()` to `close_ticket()` and updated its call sites. |
| 6 | File handling improvements | Reliability / Maintainability | Verify from original source | File operations needed proper resource management and explicit encoding. | Used context managers and explicit UTF-8 encoding. |
| 7 | Unused imports and variables | Code Quality – Pylint | Verify from before-report | Unused imports and variables create unnecessary clutter. | Removed unused imports and variables. |
| 8 | Formatting and whitespace violations | Code Style – Flake8 | Verify from before-report | Long lines, whitespace, and formatting issues reduced readability. | Corrected line lengths, whitespace, and formatting. |
| 9 | Global dictionary reassignment | Maintainability | Verify from original source | Reassigning global state in `load_tickets()` makes the function harder to reason about. | Removed the global reassignment approach. |
| 10 | Unreadable JSON output | Readability | Verify from original source | Compact JSON output is harder to inspect. | Improved JSON output readability. |
| 11 | Unclear ticket closure feedback | Usability | Verify from original source | Users need clear feedback when ticket operations succeed or fail. | Improved ticket closure feedback. |

## Static Analysis Results

| Tool | Final Result |
|---|---|
| Pylint | **10.00/10** |
| Bandit | **0 issues** (120 lines scanned in the reported run) |
| Flake8 | **0 violations** (no output) |

## Functional Testing

| Test Case | Input | Expected / Observed Result | Status |
|---|---|---|---|
| Skip closure / empty input | Empty input | Program handles skipped closure | Passed |
| Close existing ticket | `1` | `Ticket closed successfully.` | Passed |
| Close nonexistent ticket | `999` | `Ticket not found.` | Passed |

## Notes

- Exact source line numbers must be verified using the original source or before-reports.
- Bandit issue codes should be cross-checked against the saved reports.
- The before-reports have been retained unchanged.
- The fixes and test results documented here are based on the reported project work.
