# searchnapply.com

Your AI assistant searches for your next job. searchnapply.com is a job-search
connector: plug it into Claude, or into any assistant that speaks MCP, and the
assistant works your job search the way you would. It searches real openings
collected straight from company career pages, reads the ones worth reading,
watches the market for you, and tailors your resume and cover letter to the
posting you pick. Applying stays in your hands.

## Connect it

1. Create an account at https://searchnapply.com and fill in your profile once.
2. Add the connector to your assistant: https://api.searchnapply.com/mcp
   (in Claude: Settings, Connectors, Add custom connector; in Claude Code:
   claude mcp add). Any MCP client over HTTP works.
3. Sign in when the assistant asks. Every tool runs as you, nothing is anonymous.

Details and the full tool list: [docs/mcp.md](https://github.com/search-apply/.github/blob/main/docs/mcp.md).
Things to ask it: [docs/mcp-examples.md](https://github.com/search-apply/.github/blob/main/docs/mcp-examples.md).

## What your assistant can do

- Search openings by role and place, narrowed by work format, date posted,
  company, department, experience level, employment type, salary and keywords.
- Open a posting in full and send you to the company's own application page.
- Read your profile and write a resume or a cover letter tailored to a posting.
- Save a search as a monitor, check what is new, skip what you do not want,
  mark what you applied to.
- Tell you your plan, and pass your feedback to the team.

It never invents a job, a salary or a company. It reports only what
searchnapply returned.

## Where the openings come from

We read job openings directly from company career boards on the hiring
platforms most companies use (Ashby, Greenhouse, Lever, Workday,
SmartRecruiters, Workable, Personio, Recruitee, Teamtailor, iCIMS, Eightfold,
Google Careers) and refresh them through the day. No reposts from job boards,
no scraped copies of copies.

## More connectors

The same tools are coming to more ecosystems, a ChatGPT plugin first.
The short list of what is next: [docs/future-updates.md](https://github.com/search-apply/.github/blob/main/docs/future-updates.md).

## The web app

Everything the assistant does, you can also do at https://searchnapply.com:
search with the same filters, monitors with an in-app bell, a profile built
once with a guided setup and resume upload, PDF export, tailored documents to
review and edit, and a trail of every application with its status. Sign in
with email and password or with LinkedIn.

## Plans

Searching, monitors and your profile are free after sign-up. The connector
starts with a free trial, then a subscription. Paid plans, upgrades and
invoices are handled through Stripe.

## How we operate

- We respect robots.txt and the terms of every platform we read from.
- We never circumvent access controls, paywalls or security mechanisms.
- Your name, contact details and address never reach the AI model that writes
  your documents; it sees only your work content and the job.
- Your data is used to help you apply, nothing else.

## Contact

Questions, feedback, partnership: info@searchnapply.com

## Status

Live at https://searchnapply.com and evolving. Features change as real usage
teaches us what matters.
