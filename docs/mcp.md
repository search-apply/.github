# Your AI agent searches for your next job

## Connect your assistant

1. Create a searchnapply account at https://searchnapply.com and fill in your profile.
2. Add the connector in your assistant. The address is https://api.searchnapply.com/mcp.
   In Claude: Settings, Connectors, Add custom connector. In Claude Code: claude mcp add.
   Any client that speaks MCP over HTTP works.
3. Sign in when the assistant asks. The connector uses your searchnapply account; nothing works
   without it, and every tool runs as you.
4. Ask for a job. The assistant searches, reads and watches for you; applying stays with you.

Free trial, then a subscription. If the assistant says your connection expired, reconnect it the
same way.

## Description

Connect your searchnapply account and your own AI agent works your job search the way you would. It
searches postings with the same filters the site uses, opens the ones worth reading in full, and reads
your profile so it can tailor a resume or cover letter to a posting you picked. Ask it to save a search
as a monitor and it watches the market for you; check a monitor and it shows what is new; tell it to
skip a posting and that posting stops coming back. It never invents a job, a salary or a company - it
reports only what searchnapply returned, and it sends you to each posting's own job ad (postingUrl) to
apply yourself. Free trial, then a subscription.

## The twelve tools

- search_postings: totalCount, page, resolvedRole, resolvedLocations and postings, each with a one-line shortDescription.
- get_posting: one or several postings in full - employerDepartment, descriptionText and descriptionTruncated.
- get_profile: the user's profile as JSON: details, contacts, summary, skills, experience, projects, certifications, education, languages and links.
- create_monitor: the saved monitor with its id.
- update_monitor: change a saved monitor's title, place, company, keyword or filter without losing what it collected or skipped.
- list_monitors: the saved monitors with found, new, applied and skipped counts.
- delete_monitor: { deleted }.
- check_monitor: one, several or all monitors' new postings, up to limit each; reading changes nothing.
- skip_posting: skip one or many postings - { monitorId, state, done, notFound, failed }.
- mark_applied: mark one or many postings applied (undo puts them back to new) - { monitorId, state, done, notFound, failed }.
- get_subscription: the user's plan, status, trial end or renewal, and the links to prices and to manage the plan.
- send_feedback: send the user's feedback - a wrong result, a bug or an idea - to the team; returns { received, id }.

## Filters
- employment types: Full-time, Part-time, Contract, Temporary, Internship, Volunteer, Per diem, Other.
- experience levels: Internship, Entry level, Junior, Mid level, Senior, Lead, Staff, Principal, Director, Executive.
- search_postings also takes experienceLevelMin: the lowest experience level to keep, so every level at or above it is kept (min Senior keeps Senior, Lead, Staff, Principal, Director, Executive).
- departments: 27 slugs (Tech, Sales, Healthcare, ...). search_postings and create_monitor take one; a search not narrowed by department returns the top five department facets.
- a result card shows a posting's employment type and experience level in this same vocabulary.

## Links
- privacy: https://searchnapply.com/privacy
- terms: https://searchnapply.com/terms
- connector: https://api.searchnapply.com/mcp
