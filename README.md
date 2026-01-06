# AzureEventHubTutorial:

When Do You Need Ordering vs Not?

The Core Question
"If I process events out of order, will my system produce WRONG results?"
YES → You need ordering
NO → You don't need ordering

Scenarios Where You NEED Ordering ✅
1. State Transitions (Most Common)
When an entity goes through states that must happen in sequence:
Example: Order Processing

Event 1: OrderCreated (status: "pending")
Event 2: PaymentReceived (status: "paid")
Event 3: OrderShipped (status: "shipped")
Event 4: OrderDelivered (status: "delivered")

❌ WRONG ORDER = WRONG STATE!

If processed as: Event 3 → Event 1 → Event 2 → Event 4
Result: Order shows "shipped" before it was even created! 💥


2. Financial Transactions
Example: Bank Account

Starting balance: $100

Event 1: Deposit $50  → Balance: $150
Event 2: Withdraw $120 → Balance: $30
Event 3: Deposit $20  → Balance: $50

❌ WRONG ORDER:
Event 2 first → Withdraw $120 from $100 → INSUFFICIENT FUNDS! 💥
But if Event 1 processed first, it would work!

Scenarios Where You DON'T Need Ordering ❌
1. Independent Events (No State)
Example: Page View Analytics

User A views page 1 at 10:00
User B views page 2 at 10:01
User C views page 3 at 10:02

Processing order doesn't matter:
- Just counting views
- No dependency between events
- Final count is same regardless of order

✅ Process in any order: Still get correct total count

Why it works:
Events are independent
Aggregation is commutative (A+B+C = C+B+A)

2. Immutable Logs
Example: Application Logs

The Decision Matrix
Question
Need Ordering?
Does event change entity state?
✅ YES
Do later events depend on earlier ones?
✅ YES
Can events be processed independently?
❌ NO
Is it just counting/aggregating?
❌ NO
Would wrong order give wrong result?
✅ YES
Are events for same logical entity?
✅ PROBABLY
Is it time-series data?
✅ PROBABLY
Is it just logging/recording?
❌ NO

The Simple Test
Ask yourself these 3 questions:
Question 1: "Does this event change something?"
YES → Might need ordering
NO → Probably don't need ordering
Question 2: "If I process events backwards, is the result wrong?"
YES → Need ordering
NO → Don't need ordering
Question 3: "Are these events about the same thing (user, order, device)?"
YES → Probably need ordering
NO → Probably don't need ordering

Summary: The Golden Rule
"If swapping the order of two events would produce a different (wrong) final result, you need ordering."
Examples:
Swap "OrderCreated" and "OrderShipped" → WRONG ✅ Need ordering
Swap "User A viewed page" and "User B viewed page" → Same result ❌ Don't need ordering
