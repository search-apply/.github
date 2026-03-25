# Search&Apply

## Project Description — Feature Specification & User Flows

*Last updated: March 2026 — v2*

---

# 1. Project Overview

Search&Apply is a job search and application automation platform designed to eliminate repetitive work in the job application process. The app handles everything from searching for job openings across multiple platforms to generating tailored resumes and cover letters, applying on behalf of the user, managing email communication with recruiters and HR, and scheduling interviews.

## 1.1 Goals

- Simplify and automate repetitive job search and application steps.
- Improve the quality and relevance of job applications through AI-generated, tailored documents.
- Provide real, aggregated job-hiring statistics and insights based on actual application outcomes.
- Increase transparency around job market behavior (response rates, rejection timelines, market demand).

## 1.2 Compliance & Ethics

Search&Apply is designed to operate fully within legal and ethical boundaries:

- Compliance with applicable laws and regulations.
- Respect for website robots.txt rules.
- Adherence to Terms of Service / Terms of Use of all integrated platforms.
- No circumvention of access controls, paywalls, or security mechanisms.

Automation is applied responsibly, transparently, and with respect for platform policies.

---

# 2. Authentication & Account Management

## 2.1 Account Creation

Users can create an account through the following methods:

- Email and password registration with email confirmation.
- OAuth-based registration via Google, Apple, Facebook, or LinkedIn.

## 2.2 Authorization & Session Management

The app manages user sessions with access tokens and refresh tokens. Sessions are persisted securely. Token refresh is handled automatically and transparently to the user, including concurrent request handling during refresh.

## 2.3 Password Management

- Password reset via email link (expires in 15 minutes).
- Password reset via code.
- Password change from account settings (requires current password).

---

# 3. User Profile & Data

The user profile is a single scrollable page containing all information needed to generate resumes. Profile data serves as the master source for resume generation. Each section supports inline editing — the user clicks an edit button on any section, makes changes, and saves without leaving the page.

The Profile page header includes two tabs: **Profile** (resume data) and **Application Answers** (HR Q&A data for auto-filling employer forms). These are conceptually distinct: Profile = what goes on your resume, Application Answers = what goes on job application forms.

## 3.1 Profile Sections

The Profile tab displays the following sections in a single scrollable view, top to bottom:

1. **Hero:** first name, last name, middle name, headline (auto-derived from latest work experience, read-only), date of birth.
2. **Contacts:** email, phone number.
3. **Links:** resource name and URL (e.g., LinkedIn, GitHub, portfolio).
4. **Summary:** professional summary text.
5. **Skills:** top-level skills as tags.
6. **Work Experience:** company name, job title, responsibilities, start/end dates, job type, work format, skills per role, current job flag. Displayed as a list with add/edit via modal dialog.
7. **Education:** institution name, degree, field of study, start/end dates, currently studying flag. Displayed as a list with add/edit via modal dialog.
8. **Languages:** language name and proficiency level, displayed as tags.

## 3.2 Profile Data Import

Users have three options for populating their profile:

1. Fill in all data manually through the app forms.
2. Upload an existing resume in PDF or TXT format for data extraction.
3. Import profile data from LinkedIn via OAuth (goal; requires legal/partnership work). For MVP, manual entry only.

## 3.3 Employer Questions (Application Answers Tab)

The Application Answers tab (second tab under the Profile header) is where the user provides answers to common employer application questions. This data is collected once and auto-filled when the app applies to positions on behalf of the user.

Examples of questions include:

- Gender, race/ethnicity (for voluntary EEO reporting).
- Work authorization and visa status.
- Willingness to relocate.
- Salary expectations.
- Availability / earliest start date.
- Disability and veteran status.
- Any other recurring application form fields encountered across employers.

The system uses this stored data to automatically fill in application forms at apply-time. The list of supported questions will expand over time as the app encounters new fields from different employers.

---

# 4. Account Settings

Account settings are separate from feature-specific configuration. They cover everything related to the user's account and subscription within the service.

## 4.1 Account Management

- Change password.
- Manage connected OAuth accounts (link/unlink Google, Apple, Facebook, LinkedIn).
- Delete account (with confirmation dialog; permanently removes all data).
- Data export (download personal data).

## 4.2 Notification Preferences

Users configure how and when they receive notifications. Notification channels include in-app notifications and email. Events that trigger notifications:

- New job opening found matching a search query.
- Documents (resume/cover letter) generated and ready for review.
- Application submitted on behalf of the user.
- Important email received from a recruiter or HR.
- Interview scheduled or calendar event created.
- Application status change (e.g., rejection received).

Users can enable or disable notifications per event type and per channel.

## 4.3 Subscription & Billing

The app offers tiered subscription plans. Pricing will be determined based on hosting costs and market research (target: no more than $50/month for the highest tier). Subscription tiers:

1. **Free Tier:** limited functionality, basic job search, manual application only.
2. **Passive Search:** automated job monitoring with notifications; documents generated but user applies manually.
3. **Active Search:** full automation including document generation and application submission.
4. **"I Need a Job Right Now":** highest priority processing, maximum query limits, full automation with email handling.

Exact feature limits per tier (number of active queries, applications per month, AI document generations, email features) are to be defined based on infrastructure costs and competitive analysis.

Subscription management includes: view current plan, upgrade/downgrade, billing history, and payment method management. Accessible as a standalone page via `/subscription` route.

---

# 5. Job Search & Queries

The core feature of the app. Users create search queries that monitor the job market across multiple platforms and return matching openings.

**Screen description:** The Job Search page opens to a list of the user's saved search queries displayed as cards. Each card shows the query name, key preferences, and status. Clicking a query opens its detail view with editable search preferences, apply mode selector, AI document configuration, email configuration, and notification toggles. Running a query displays matching job openings as a scrollable list, where each result shows job title, company, location, salary (if available), and action buttons (flag for review, view details).

## 5.1 Search Query Creation

Users can create and run multiple job search queries simultaneously. For example, one query for "QA Engineer in Los Angeles, CA" and another for "SDET in California" with different preferences.

## 5.2 Search Preferences

Each query has configurable preferences:

- Job title / keywords.
- Company: target specific companies or exclude specific companies.
- Location: city, state, country, or radius.
- Salary range.
- Work format: on-site, hybrid, remote.
- Job type: full-time, part-time, contract, internship.
- Experience level: junior, mid-to-senior, director, intern.
- Keyword inclusion/exclusion: job descriptions must include or must not include specific terms.

## 5.3 Search Sources

The app aggregates job postings from multiple sources:

- LinkedIn job postings.
- Indeed.
- Company career pages powered by Workday, Greenhouse, Lever, and similar ATS platforms.
- Direct company job boards.

Source coverage will expand over time. Initial focus is on the most popular platforms where automated application is feasible.

## 5.4 Query-Level Configuration

Each search query can have its own settings for:

### 5.4.1 Apply Mode

Three modes of operation per query:

**Full Manual:** The app searches for positions and prepares a resume + cover letter. The user reviews everything and applies to the position himself.

**Fully Automated ("Do It for Me"):** The app searches, generates documents, and applies to every matching position automatically.

**Wise:** The user flags specific companies as "always review." For flagged companies, the user must review and approve documents before the app applies. For all other companies, the app applies automatically. Initially, flagging is done inline from search results. A dedicated company watchlist management page may be added later.

### 5.4.2 AI Document Configuration

- Enable or disable AI-generated resume tailoring per query.
- Enable or disable AI-generated cover letter per query.
- The AI uses profile data, job description, and company public information (vision, values, culture) to generate tailored documents.

### 5.4.3 Email Configuration (per query)

- Choose a mailing strategy for this query (e.g., follow-up timing, tone).
- Choose email templates for outreach and responses.

## 5.5 Notification per Query

Each query has its own notification settings: notify when new matching openings are found, notify when documents are ready, notify when an application is submitted.

---

# 6. AI Configuration

AI is used to generate resumes, cover letters, and email responses. Users can configure the AI's writing style to match their personal voice.

## 6.1 Writing Style Settings

Separate writing style configurations for:

1. **Resume writing style:** how the AI phrases accomplishments, responsibilities, and summaries on the resume.
2. **Cover letter writing style:** tone, formality, and structure of generated cover letters.
3. **Email writing style:** tone and approach for recruiter/HR email responses.

## 6.2 Style Configuration Options

For each writing style, the user can:

- Select from preset styles: Professional, Friendly, Concise, Technical, Creative.
- Provide a free-text description of their desired voice and tone.
- Upload a writing sample that the AI will analyze and mimic.

All three options can be combined. Presets serve as a baseline, free-text refines it, and writing samples provide the most personalized calibration.

---

# 7. Resume & Cover Letter Generation

## 7.1 Resume Generation

The user's profile data is the master resume. When AI tailoring is enabled, the app generates a position-specific resume for each job opening by:

- Using all profile data (experience, skills, education, summary) as the base content.
- Analyzing the job description for required skills, keywords, and emphasis areas.
- Rewriting and reordering content to best match the specific position.
- Applying the user's configured resume writing style.

The user can review and edit any generated resume before it is used for an application (depending on the apply mode).

## 7.2 Cover Letter Generation

Cover letters are generated per application using:

- The user's personal details and professional summary from their profile.
- The job description and requirements.
- Company public information: company vision, values, culture, mission statement (scraped from the company's public website and career pages).
- The user's configured cover letter writing style.

Company data collection is a planned feature. Initially, cover letter generation relies on job description and profile data only.

---

# 8. My Applications

The central hub for tracking all job applications. Documents (generated resumes and cover letters) are attached to each application rather than living on a separate page.

**Screen description:** My Applications is a filterable list view. The default view shows all applications sorted by date, with filter controls for query, company, status, and date range. Each row shows the company name, job title, status badge, applied date, and attached document indicators. Clicking a row opens the application detail view, which displays position information at the top, attached resume and cover letter with preview/edit/download actions in the middle, and the email conversation thread (if applicable) at the bottom.

## 8.1 Application Tracking

Each application is tracked with the following statuses:

1. **Job Opening Found:** a matching position has been identified by a search query.
2. **Documents Generated:** resume and/or cover letter have been created for this position.
3. **Applied:** the application has been submitted.
4. **Rejected:** a rejection has been received (detected from email or manually marked by the user).
5. **Offered:** the user has received an offer (user-reported).
6. **Hired:** the user has accepted an offer (user-reported).
7. **User Rejects Offer:** the user has declined an offer (user-reported).

Later statuses (Offered, Hired, User Rejects Offer) depend on the user's willingness to update the system. The app may detect some of these from email content, but will not aggressively track beyond what the user shares.

## 8.2 Application Organization

Applications can be sorted and filtered by:

- Search query (which query found this position).
- Company name.
- Date (applied date, found date).
- Status.
- Additional sort/filter criteria may be added as needed.

## 8.3 Attached Documents

Each application entry includes:

- The tailored resume used (or to be used) for this application.
- The tailored cover letter used (or to be used) for this application.
- The user can view, edit, and download these documents from the application detail view.

---

# 9. Email Integration & Communication

Email is used both for applying to positions and for ongoing communication with recruiters and HR. This feature comes after MVP and after basic application handling is live.

## 9.1 Email Setup

The user configures an email to be used for job applications. Options:

1. Create a new Gmail account and provide credentials to the app.
2. The app creates an email on its own domain and provides credentials to the user.

A separate email dedicated to the hiring process is recommended but not required. The user's email will be used to create accounts on job boards and to communicate with employers.

## 9.2 Email Conversation Management

- All email conversations are organized by position and company, linked to the corresponding application in My Applications.
- The user can pick up a conversation manually at any point and hand it back to AI at any point.
- Auto-responding to incoming recruiter emails can be enabled or disabled.
- Email templates are available for common responses.

## 9.3 Email Writing Style

Email tone and style follow the user's configured email writing style (see Section 6: AI Configuration).

---

# 10. Calendar Integration

If the user has granted email access and the app is managing recruiter conversations, the app can detect interview scheduling and automatically create calendar events.

- Supported calendars: Google Calendar, Apple Calendar, Outlook (to be determined based on implementation complexity).
- The app reads email conversations to detect interview invitations and proposed times.
- Upon detecting an interview, the app creates a calendar event with date, time, company name, and any relevant details.
- This feature depends on email integration being active and is not part of MVP.

---

# 11. Statistics & Analytics

The app provides two types of analytics.

**Screen description:** The Statistics page is split into two views accessible via tabs or toggle: Personal Statistics (the user's own application funnel and activity metrics) and Market Insights (per-position and aggregate data). Personal stats show summary cards at the top (total apps, response rate, interview rate) with a visual funnel chart below. Market insights are accessible per job posting from search results or the application detail view.

## 11.1 Personal Statistics

A dashboard showing the user's own application activity:

- Total applications sent.
- Response rate (applications that received any response).
- Interview conversion rate.
- Average time to hear back.
- Applications by platform/source.
- Applications by status (visual funnel).

## 11.2 Market / Position Insights

Per-position and market-level data aggregated from all users and public sources:

- Number of users who applied for a given position through Search&Apply.
- Public data about the position from LinkedIn, Indeed, and other platforms (e.g., total applicant count where available).
- Market trends: demand by role, location, and salary ranges.

Market insights grow more valuable as the user base grows. Initial implementation may be limited to personal statistics.

---

# 12. Public Job Search Page

A free, publicly accessible page where anyone can search for open positions across all sources the app aggregates. No account required.

- Search-only: no application, document generation, or account features.
- Purpose: attract new users to the platform by providing value before signup.
- Implementation is deferred until after production launch with initial users, when the app has built a pool of aggregated job openings to display.

---

# 13. User Flows

## 13.1 Onboarding Flow (MVP)

1. User visits the landing page and clicks "Get Started."
2. User creates an account via email/password or OAuth.
3. User confirms email (if email registration).
4. User lands on the Profile page.
5. User fills in personal information, summary, work experience, education, skills, and links.
6. User navigates to the Application Answers tab and fills in common HR question answers.

Note: A guided onboarding wizard with progress indicators is planned for a later release.

## 13.2 Job Search & Document Generation Flow (MVP)

1. User navigates to Job Search.
2. User creates a new search query with job title, location, preferences, and filters.
3. User selects an apply mode for this query: Full Manual, Fully Automated, or Wise.
4. User enables or disables AI resume tailoring and cover letter generation for this query.
5. The app runs the query and returns matching job openings.
6. For each match, the app generates a tailored resume and cover letter (if enabled).
7. User reviews generated documents in the My Applications section.
8. The user can edit documents before applying.

## 13.3 Application Flow

**Full Manual mode:**

1. User sees matched openings with generated documents.
2. User reviews resume and cover letter for each position.
3. User downloads the docs and applies himself.

**Fully Automated mode:**

1. App finds matching openings.
2. App generates documents.
3. App applies automatically to all matches.
4. User is notified of each application submitted.

**Wise mode:**

1. App finds matching openings.
2. App generates documents.
3. For companies flagged as "always review": the user receives a notification, reviews documents, and manually approves before the app applies.
4. For all other companies, the app applies automatically.
5. User is notified of all applications.

## 13.4 Email Communication Flow (Post-MVP)

1. User sets up an email account for job applications (see Section 9.1).
2. The app monitors the inbox for recruiter and HR responses.
3. Incoming emails are linked to the corresponding application in My Applications.
4. If auto-responding is enabled, the AI drafts and sends replies using the user's email writing style.
5. User can intervene at any point: read the conversation, edit a draft, send manually, or hand back to AI.
6. If an interview is detected in the email thread, the app creates a calendar event (if calendar integration is active).

## 13.5 Application Tracking Flow

1. User navigates to My Applications.
2. User sees all applications organized by query, company, date, or status.
3. User clicks on an application to see details: position info, attached resume, attached cover letter, email thread (if applicable), and current status.
4. User can manually update status (e.g., mark as "Offered" or "Hired").
5. User can download or edit the attached documents.

---

# 14. MVP Scope

The Minimum Viable Product focuses on the core loop: onboard, search, and generate documents.

## 14.1 In Scope for MVP

- Account creation (email + OAuth).
- User profile: all sections (Hero, Contacts, Links, Summary, Skills, Experience, Education, Languages).
- Employer questions (Application Answers tab — HR Q&A data collection).
- Job search query creation with all search preferences.
- AI-powered resume tailoring per job opening.
- AI-powered cover letter generation per job opening.
- Document review and editing before application.
- Manual profile entry (no LinkedIn/Indeed import in MVP).

## 14.2 Post-MVP Phases

**Phase 2 — Application Handling:** Automated application submission to popular job boards and ATS platforms. My Applications tracking with status management. Apply modes (Manual, Automated, Wise).

**Phase 3 — Email Integration:** Email setup and inbox monitoring. AI-powered email responses. Email conversation management linked to applications.

**Phase 4 — Advanced Features:** Calendar integration for interview scheduling. Statistics and analytics (personal + market). Subscription tiers and billing. Public job search page. LinkedIn OAuth profile import. Company data collection (vision, values, culture). Guided onboarding wizard. LinkedIn network expansion and recruiter conversations.

---

# 15. Tech Stack

## 15.1 Back End

- .NET 9 / C# 12
- PostgreSQL
- Kafka / NATS (message broker)
- Clean Architecture: API layer, Application layer, Domain layer, Infrastructure layer.
- Microservices: separate services for Auth, Profile, Job Queries, Job Postings (each with its own API contract and OpenAPI spec).

## 15.2 Front End

- TypeScript, React, Next.js
- Bun as runtime and package manager.
- TanStack Query for API state management.
- OpenAPI-generated API clients (auto-generated from backend specs).
- Tailwind CSS with shadcn/ui component library.
- Playwright for end-to-end testing.

## 15.3 Infrastructure

Local:
- Docker / Docker Compose for containerized development and deployment.
- Multi-stage Dockerfile: base, dependencies, build, production, test stages.
- Serilog + OpenTelemetry for structured logging.
- Seq for log aggregation.

Prod:
- AWS EKS cluster

---

# 16. Application Structure & Navigation

## 16.1 Public Pages (no auth required)

- Landing / Home page with feature overview and roadmap.
- Sign Up page.
- Sign In page.
- Public Job Search page (deferred).

## 16.2 Protected Pages (auth required)

Accessible via a sidebar navigation:

- **Profile:** two-tab layout under a shared header. The **Profile** tab is a single scrollable page with inline-editable sections (Hero, Contacts, Links, Summary, Skills, Experience, Education, Languages). The **Application Answers** tab contains pre-filled answers to common employer form questions (HR Q&A).
- **Job Search:** query list as cards, query detail view with search preferences and per-query configuration (apply mode, AI settings, email settings, notifications), search results list.
- **My Applications:** filterable application list with sorting by query/company/date/status, application detail view with attached documents (resume + cover letter) and email thread.

## 16.3 Account Settings

Accessible from the profile or a dedicated settings area:

- Password management.
- Connected accounts (OAuth).
- Notification preferences.
- Subscription and billing (also accessible via standalone `/subscription` page).
- Delete account.

---

# 17. Sources & Links

- GitHub: https://github.com/search-apply
- Figma Prototype: https://www.figma.com/proto/qEcKkOSackI32wYAWjePUn

---

# 18. Possible Future Features

- Company data scraping: automated collection of company vision, values, and culture from public sources for improved cover letter generation.
- Public job search page as a user acquisition funnel.
- More data on job openings: how many times an opening was republished, ghosting detection, etc.
- **Hiring platform (long-term vision):**
  - Companies could post jobs exclusively on the platform.
  - Companies will be able to see a list of candidates that align with their requirements.
  - Employees will be able to set expected salary range and an "open to opportunities" status.
  - With this data, companies will have a curated list of candidates to reach out to.
- LinkedIn network expansion: automated connection requests to expand professional network.
- LinkedIn conversations with recruiters: AI-managed outreach and follow-up via LinkedIn messaging.
- Advanced onboarding wizard with progress tracking.
- Multiple resume/cover letter base templates.
- Resume visual themes and formatting options.
