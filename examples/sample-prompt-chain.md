# Example: Prompt Chain for a Small Feature

This is a worked example of the "feature implementation" template in action, using a generic but realistic .NET/Azure scenario. Replace with your own real chain when you have one — see `docs/04-case-study.md`.

## Step 1 — Scope (written by hand, no AI)

> Add a method to cancel a pending order if it hasn't shipped yet. Must not allow cancellation once an order's status is "Shipped" or later. Needs to update OrderStatus and write an audit log entry. Existing OrderService class already has similar status-transition methods to match style against.

## Step 2 — Draft prompt

```
Context: ASP.NET Core service layer, Azure SQL via EF Core.
Existing pattern: see OrderService.MarkAsShippedAsync for the status-transition style already used in this class.
Task: implement OrderService.CancelOrderAsync(orderId) that cancels a pending order.
Constraints:
- Only allow cancellation if current status is "Pending" or "Processing"
- Throw InvalidOperationException with a clear message if status is "Shipped" or later
- Write an audit log entry via the existing IAuditLogger interface
Required: unit tests covering each status value, including the boundary case of "Processing"
```

## Step 3 — What came back (summarized)

The model produced the method, matched the existing pattern reasonably well, and included tests for "Pending" and "Shipped" — but skipped the boundary case of "Processing" entirely, despite it being explicitly requested.

## Step 4 — Review catch

Caught on review: the missing "Processing" test case, plus the audit logger call was added *after* the database save rather than as part of the same transaction — meaning a failure between the two steps would leave an inconsistent state.

## Step 5 — Guardrail produced

Added to the guardrails list: any state-changing method that also writes an audit log gets checked for whether the two operations are properly transactional — this is an easy thing for AI-generated code to get subtly wrong because both calls "look" sequential and correct on the surface.
