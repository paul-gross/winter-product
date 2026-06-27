# Writing Style

Plans should focus on **correctness of domain models** and **high-level logic**, not language-specific implementation details.

## Domain Models

Define the structure and relationships of entities clearly:
- Entity names and their purpose
- Key properties and their types
- Relationships between entities (one-to-many, many-to-many, etc.)
- Constraints and business rules

Use language-agnostic representation or simple class diagrams when possible.

## Pseudocode Over Code

Describe logic using **bulleted lists and plain English**, not language-specific syntax:

**Good — Bulleted Pseudocode:**
```
Processing Pending Notifications:
- For each undelivered notification in the queue:
  - Check user's notification preferences
  - If user has opted in for this notification type:
    - Format the notification for the delivery channel
    - Deliver the notification
    - Mark as sent with timestamp
    - If delivery fails, increment retry count
```

**Avoid — Language-Specific Code:**
```python
def process_pending_notifications():
    for notification in get_undelivered_notifications():
        prefs = get_user_preferences(notification.user_id)
        if prefs.is_opted_in(notification.type):
            formatted = format_notification(notification, prefs.channel)
            send_notification(formatted)
```

## Why This Approach?

1. **Language Agnostic**: Plans can be implemented in any language
2. **Focus on Logic**: Emphasizes the "what" and "why" over syntax
3. **Easier to Review**: Non-developers can understand the approach
4. **More Flexible**: Allows implementation flexibility within the framework

## When to Show Code

Use actual code blocks only for:
- Domain model structure (to show properties clearly)
- Database schema definitions
- API contract examples
- Configuration formats

Even in these cases, prefer simple, readable examples over complete implementations.
