# What to ask your assistant

One line per request, and the tool the assistant reaches for. The names in the examples are made up.

| You say | What happens |
|---|---|
| "Find senior .NET jobs in Berlin, remote ok, posted this week." | search_postings: a list, one line per posting, with links |
| "Open the second one in full." | get_posting: the whole posting text |
| "Which of these fit my profile best?" | get_profile, then the assistant compares |
| "Write a cover letter for it." | get_profile and get_posting, then the assistant writes |
| "Watch this search for me." | create_monitor: a saved monitor that keeps collecting |
| "Anything new on my monitors?" | check_monitor: the postings you have not handled yet |
| "Skip the first two." | skip_posting: they stop coming back |
| "I applied to the Northwind one." | mark_applied: moved to applied, undo puts it back |
| "Add Kubernetes to my Berlin monitor." | update_monitor: the monitor changes, nothing collected is lost |
| "What am I watching?" | list_monitors: every monitor with its counts |
| "What plan am I on?" | get_subscription: plan, status, where to manage it |
| "Tell the team the salary on that posting is wrong." | send_feedback: delivered to us with the posting |

The assistant never applies for you and never invents a posting. When results are thin, ask for a
neighbouring role: a job is often filed under SDET, QA engineer and test engineer at once.
