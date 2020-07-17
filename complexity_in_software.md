# Where does complexity go to after us making our decisions?

`Complaints`

|status(enum)| reminds_at |
| ---- | ---------- |
| pending, in_progress, closed | DateTime |

`Tickets`

|status(enum)| reminds_at |
| ---- | ---------- |
| todo, ongoing, closed | DateTime |

I keep having this question when I introduce moving parts into my codebase.
The easiest example that I can take is the recent project that I worked on.
Tickets, Complaints and their management system.

In the projects, we can see how both data models handle the statuses.

In complaints, we have "pending", "in_progress" and "closed" in the DB, which,
along with field "reminds_at" is used to represent the ticket statuses
"pending", "todo", "ongoing" and "closed" for the business.

The "todo" and "ongoing" for the business is indicated by the "in_progress" and "reminds_at" fields in the DB.
When querying for the data, we build a "large-ish" SQL query(not unmaintainable). and present it to our users.

And now we come to the tickets model, where we needed something similar.
With tickets, we have "TODO", "ONGOING" and "CLOSED"

A ticket moves between the TODO and ONGOING states(open states), based on the "reminds_at" and "assigned_agent" values.
Each of these states are set and not calculated, based on user actions.

For this, we have 12 different state transitions(7 ways to set them), based on different conditions, and a rake task that does one of these as well.
All of state transition and setting because we wanted to avoid writing a complex query to fetch and display tickets.
Even though introducing an extra state has simplified our queries, I think we have introduced a lot more complexity else where in the process.

Thus, we come back to my question, where does the complexity go to after we make our decisions.

Afterword: I would have liked it the complexity lived in the querying part, and we had our ticket model store only `open` and `closed` as states instead of 3
