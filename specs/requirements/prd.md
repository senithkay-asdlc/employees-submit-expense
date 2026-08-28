# Employees Submit Expense — PRD

## Problem Statement

Employees pay for business expenses out of pocket and today rely on ad-hoc
spreadsheets, emails, or paper forms to request reimbursement. Managers have
no single place to review and approve these requests, and finance has to
manually chase approved amounts and re-key them into payroll. This is slow,
error-prone, and leaves no clear audit trail of who approved what and when.

## Solution

A system where employees submit expense claims online, their manager reviews
and approves or rejects each claim, and finance exports the batch of approved
claims as a file ready to feed into payroll — replacing the spreadsheet/email
shuffle with a single tracked workflow from submission to payroll handoff.

## Actors

- **Employee** — submits expense claims, tracks their status, and can correct
and resubmit a rejected claim.
- **Manager** — reviews expense claims submitted by the employees assigned to
them, and approves or rejects each one.
- **Finance** — views approved claims, exports them as a payroll-ready file,
and marks them as exported once handled.
- **Admin** — assigns each employee to the manager who approves their claims.

## User Stories

1. As an Employee, I want to submit an expense claim with an amount, category,
date, and description, so that I can request reimbursement.
2. As an Employee, I want to attach a receipt to my expense claim, so that I
can provide proof of purchase.
3. As an Employee, I want to view the status of my submitted claims (pending,
approved, rejected, exported), so that I know where each one stands.
4. As an Employee, I want to edit and resubmit a rejected claim, so that I can
correct the issue my manager flagged instead of starting over.
5. As a Manager, I want to see the pending expense claims submitted by the
employees assigned to me, so that I know what needs my review.
6. As a Manager, I want to approve or reject a claim with an optional comment,
so that the employee understands the decision.
7. As a Finance user, I want to see all approved claims, so that I can prepare
the next payroll export.
8. As a Finance user, I want to export approved claims as a downloadable file
(e.g. CSV), so that I can bring them into payroll.
9. As a Finance user, I want exported claims marked as exported, so that they
are not accidentally exported twice.
10. As an Admin, I want to assign a manager to each employee, so that claims
route to the correct approver.

## Product Decisions

- Sign-in is via SSO through Thunder, the platform IDP (org default).
- Approval is single-tier: one manager approval moves a claim to approved:
ready for finance export. No secondary finance sign-off or amount-based
routing.
- Employee-to-manager assignment is pre-configured by an Admin rather than
inferred or self-selected; a claim routes to whoever the employee's admin-
assigned manager is.
- Finance exports approved claims as a downloadable CSV file; there is no
direct integration with a specific payroll system.
- A receipt attachment is supported on every claim but is optional — a claim
can be submitted without one.
- A rejected claim can be edited and resubmitted by the employee rather than
requiring a brand-new claim.
- Expense claims use a fixed set of categories: Travel, Meals, Lodging,
Supplies, Other.
- All claims are in a single organization-wide currency; no multi-currency
handling. *assumed*
- Status-changing actions (submission, approval, rejection) notify the
relevant actor by email.

## Out of Scope

- Direct API integration with a specific payroll platform.
- Multi-level or amount-based approval routing.
- Actual payment/reimbursement processing — the system stops at handing
finance an export-ready file.
- Multi-currency expense claims.
- Mobile app (web only).
- Self-service manager selection or org-chart management beyond the simple
employee → manager assignment.

## Open Questions

1. Should there be a limit or policy on expense amounts (e.g. per-category
caps) that triggers a warning or block at submission time?

## Further Notes

None.