--- 
sidebar_position: 4
title: Tickets
---

# Tickets Settings 

# Tickets
| Setting | Default | Description |
| --- | --- | --- |
| Default Ticket Type | `Issue` | The default ticket type for newly created tickets. |
| Allow Public Tickets | `false` | Allow unregistered users to create tickets. A user account will automatically generate for that user base on their email |
| Allow Agents to Submit Tickets on Behalf of Users | `true` | Allow agents to submit tickets as another user. |
| Show Overdue Tickets | `true` | Shows a blinking ticket row on the tickets page if a ticket is in violation of its SLA time |
| Minimum Subject Length | `10` | The minimum character length the subject must meet in order for the ticket to validate successful. |
| Minimum Issue Length | `10` | The minimum character length the issue must meet in order for the ticket to validate successful. |

## Ticket Types
Ticket Types are categories of tickets that link **priorities** with SLA times to tickets. Allowing administrators to setup different types of tickets with different SLA requirements. The default `Issue` and `Task` ticket type share the same priorities and act a way to group tickets together.

## Priorities
Ticket priorities define the response time or SLA of the ticket via its **Ticket Type**. Once a ticket is in violation of its SLA time, it will automatically be marked as an overdue ticket. 

## Ticket Tags
Tags are used to group tickets together. Tags are used in reporting and filter of tickets. A **Top 10 Tags** chart is also displayed in on the Dashboard to show which issues are more common.