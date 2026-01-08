# XploreSTEMi Competition Platform - Product Requirements Document

**Version:** 1.0  
**Date:** January 8, 2026  
**Project Duration:** 3 Days  
**Owner:** Joshua (XploreSTEMi)

---

## Table of Contents
1. [Executive Summary](#executive-summary)
2. [Product Vision & Goals](#product-vision--goals)
3. [User Personas](#user-personas)
4. [Core Features & Requirements](#core-features--requirements)
5. [Technical Architecture](#technical-architecture)
6. [User Flows](#user-flows)
7. [Data Models](#data-models)
8. [UI/UX Requirements](#uiux-requirements)
9. [Security & Permissions](#security--permissions)
10. [Development Roadmap](#development-roadmap)
11. [Success Metrics](#success-metrics)
12. [Future Enhancements](#future-enhancements)

---

## Executive Summary

XploreSTEMi Competition Platform is a web-based application enabling STEM competitions for students across schools and globally. The platform supports two competition types (coding challenges and project-based tasks) and two participation modes (in-school and global competitions), fostering skill development and healthy competition among students.

**Key Differentiators:**
- Dual-mode competition system (in-school vs global)
- Multi-format submissions (code, reports, videos)
- Hybrid judging system (automatic, manual, peer-review)
- Built for non-profit scalability with minimal operational overhead

---

## Product Vision & Goals

### Vision
Empower students worldwide to showcase their STEM skills through accessible, engaging competitions that recognize excellence and foster learning.

### Primary Goals
1. Launch MVP within 3 days with core competition features
2. Enable XploreSTEMi facilitators to create and manage competitions effortlessly
3. Provide seamless experience for students to participate and track progress
4. Scale from school-level to global competitions without platform limitations
5. Maintain zero-cost operations during testing phase

### Success Criteria
- Platform handles 50+ simultaneous participants per competition
- Competition creation takes <5 minutes
- Submission process takes <10 minutes
- 95%+ uptime during competition windows
- Mobile-responsive experience

---

## User Personas

### 1. XploreSTEMi Facilitator (Admin)
**Profile:** 25-35 years old, STEM educator, manages school clubs or global programs  
**Goals:**
- Create competitions quickly with clear requirements
- Monitor participant progress in real-time
- Manage judging workflows efficiently
- Generate reports and analytics
- Award prizes to winners

**Pain Points:**
- Manual tracking across multiple platforms
- Difficulty managing different competition types
- Time-consuming result compilation

### 2. School Club Coordinator
**Profile:** 18-22 years old, student leader at XploreSTEMi club  
**Goals:**
- Oversee in-school competitions
- Help peers with submission issues
- Monitor school leaderboard
- Communicate with facilitators

**Pain Points:**
- Lack of visibility into competition status
- Manual student verification

### 3. Student Participant
**Profile:** 14-22 years old, high school/early university, varying technical skills  
**Goals:**
- Discover relevant competitions easily
- Submit work confidently
- Track progress and rankings
- Learn from competition experience
- Win prizes and recognition

**Pain Points:**
- Confusing submission requirements
- Unclear competition rules
- Delayed feedback on submissions

### 4. Peer Reviewer/Judge
**Profile:** 20-30 years old, advanced student or alumni  
**Goals:**
- Evaluate submissions fairly
- Provide constructive feedback
- Complete reviews efficiently

**Pain Points:**
- Unclear evaluation criteria
- Overwhelming number of submissions

---

## Core Features & Requirements

### 1. User Authentication & Profiles

#### User Types
- **Super Admin** (XploreSTEMi Core Team)
- **Facilitator** (Competition Creators)
- **School Coordinator** (Club Leaders)
- **Participant** (Students)
- **Judge** (Peer Reviewers)

#### Authentication Features
- Email/password registration
- OAuth (Google Sign-In for students)
- Email verification
- Password reset functionality
- Role-based access control (RBAC)

#### Profile Information
**All Users:**
- Full name
- Email
- Profile picture (optional)
- Country
- Bio (optional)

**Students Additional:**
- Age/Date of birth
- School/Institution
- Grade level
- Skills/interests tags
- Competition history
- Points/badges earned

**Facilitators Additional:**
- Organization affiliation
- Competitions created count
- Schools managed

---

### 2. Competition Management System

#### Competition Types

##### A. Coding/DSA Competition
**Format:** Timed challenge with algorithmic problems

**Key Features:**
- Problem statement with test cases
- Code editor integration (Monaco Editor or embed Judge0)
- Multiple language support (Python, JavaScript, C++, Java)
- Automatic test case validation
- Time tracking (start to submission)
- Leaderboard (ranked by time + correctness)
- Submission history

**Configuration Options:**
- Time limit (e.g., 2 hours)
- Problem difficulty level
- Test case visibility (sample vs hidden)
- Allowed programming languages
- Penalty for wrong submissions

##### B. Project/Task-Based Competition
**Format:** Open-ended challenges with multi-format submissions

**Key Features:**
- Rich text problem description with media support
- Multiple submission types:
  - Code repository (GitHub/GitLab link)
  - Written report (PDF/DOC upload, max 10MB)
  - Video demo (YouTube/Vimeo link or upload, max 100MB)
- Rubric-based evaluation
- Deadline management
- Submission versioning (allow resubmission before deadline)

**Configuration Options:**
- Submission deadline
- Required vs optional submission types
- Max team size (solo, pairs, teams)
- Evaluation criteria/rubric
- Resource limits (file sizes)

#### Competition Modes

##### A. In-School Competition
**Scope:** Restricted to students from specific school

**Features:**
- School-specific registration codes
- School leaderboard
- Club coordinator oversight dashboard
- School-level prizes
- Facilitator can monitor school progress

**Workflow:**
1. Facilitator creates competition
2. Assigns to specific school(s)
3. Generates unique registration code per school
4. Students register using school code
5. Competition runs with school-only visibility
6. Results shared with school first, then globally

##### B. Global Competition
**Scope:** Open to all registered users

**Features:**
- Public registration (no code needed)
- Global leaderboard
- Country/region filters
- Higher prize tiers
- Featured on homepage

**Workflow:**
1. Facilitator creates competition
2. Sets as "Global" mode
3. Competition appears on public competition list
4. Any verified user can join
5. Results displayed globally

#### Competition States
- **Draft:** Facilitator is creating (not visible to participants)
- **Published:** Visible and open for registration
- **Active:** Competition is live, submissions accepted
- **Judging:** Submission closed, evaluation in progress
- **Completed:** Results published, winners announced
- **Archived:** Past competitions for reference

#### Competition Creation Workflow
1. Select competition type (Coding or Project)
2. Select mode (In-School or Global)
3. Fill competition details:
   - Title
   - Description
   - Banner image
   - Difficulty level (Beginner/Intermediate/Advanced)
   - Tags (e.g., AI, Web Dev, Robotics)
4. Configure settings (time, deadlines, languages, etc.)
5. Set evaluation criteria/rubric
6. Define prizes
7. Preview and publish

---

### 3. Judging & Evaluation System

#### Automatic Judging (Coding Competitions)
**System:**
- Integration with Judge0 API or similar
- Test case execution in sandboxed environment
- Immediate feedback on correctness
- Time penalties for multiple attempts
- Anti-plagiarism checks (basic code similarity detection)

**Scoring Algorithm:**
```
Score = (Correctness × 60%) + (Speed × 30%) + (Code Quality × 10%)
```

#### Manual Judging (Project Competitions)
**Rubric System:**
- Facilitator defines evaluation criteria (e.g., Innovation: 30%, Implementation: 40%, Presentation: 30%)
- Each criterion scored on scale (e.g., 1-10)
- Judge provides written feedback per criterion
- Overall score auto-calculated from weighted criteria

**Judge Dashboard:**
- List of submissions to review
- Side-by-side view: submission + rubric
- Progress tracker (X of Y submissions reviewed)
- Save draft reviews
- Submit final review

#### Peer Review (Optional)
**System:**
- Each participant reviews 2-3 peer submissions (anonymous)
- Simplified rubric (3-5 key criteria)
- Peer scores weighted at 20% of final score
- Facilitator scores weighted at 80%
- Prevents self-review and reviews from same school (conflict of interest)

**Quality Control:**
- Flag inappropriate reviews
- Facilitator can override peer scores
- Minimum character count for feedback (50 words)

---

### 4. Submission System

#### Submission Workflow
1. Student clicks "Submit" from competition page
2. Uploads required materials:
   - **Coding:** Paste code or upload file + select language
   - **Project:** Upload report + paste repo link + paste video link
3. Preview submission
4. Confirm and submit
5. Receive confirmation email
6. View submission status (Submitted → Under Review → Graded)

#### Features
- Drag-and-drop file uploads
- Real-time file validation (size, type)
- Progress bars for uploads
- Submission receipt/confirmation number
- Edit/resubmit before deadline
- Submission timestamp (to detect late submissions)

#### Constraints
- Max file sizes: Reports (10MB), Videos (100MB if uploaded, unlimited if linked)
- Accepted formats: PDF, DOCX for reports; MP4, MOV for videos
- Code submissions: Plain text or .zip with source files

---

### 5. Leaderboard & Results

#### Real-Time Leaderboard (Coding Competitions)
**Display:**
- Rank, username, score, time taken, problems solved
- Live updates during competition
- Filter by school (for in-school competitions)
- Filter by country (for global)

**Privacy:**
- Show top 10 always
- Show user's rank always
- Option to hide real names (show usernames only)

#### Results Page (All Competitions)
**Components:**
- Winners podium (Top 3 with profile pics)
- Full rankings table (paginated)
- Prize distribution details
- Winner highlights/testimonials
- Download certificate option for participants

#### Analytics Dashboard (Facilitator)
- Total participants
- Submission rate (submitted vs registered)
- Average scores
- Completion time distribution
- Participation by school/country
- Export to CSV

---

### 6. Prize & Rewards System

#### Prize Types
- **Cash prizes:** Displayed prominently (e.g., "$500 for 1st place")
- **Certificates:** Auto-generated PDFs with competition details
- **Badges:** Digital badges for profile (e.g., "Top 10 Finisher", "Fastest Solver")
- **Swag:** Physical items (tracked separately, not in-app fulfillment)

#### Prize Configuration (Facilitator)
- Set prize per rank (1st, 2nd, 3rd, Top 10, etc.)
- Add sponsor logos to certificates
- Choose badge designs from template library

#### Prize Fulfillment
- Manual process: Facilitator marks prizes as "Awarded"
- Email notification to winners with claim instructions
- Track fulfillment status (Pending → Shipped → Delivered)

---

### 7. Notification System

#### Notification Types
- Competition published (for global) or school code shared (for in-school)
- Competition starting soon (24hrs, 1hr reminders)
- Submission deadline approaching (24hrs, 1hr warnings)
- Submission received confirmation
- Judging complete, results available
- Prize awarded
- New comment/feedback on submission

#### Delivery Channels
- **In-app notifications:** Bell icon with unread count
- **Email notifications:** User can opt-in/out per type
- **Push notifications (future):** For mobile app

---

### 8. Communication Features

#### Discussion Forums (Per Competition)
- Q&A section for clarifications
- Facilitator can post announcements
- Students can ask questions (public or private to facilitator)
- Upvote helpful questions

#### Direct Messaging
- Students can message facilitators
- Facilitators can message participants (bulk or individual)
- No student-to-student messaging (to prevent cheating)

#### Feedback System
- Judges leave feedback on submissions
- Students can reply to feedback (not to change score, just for learning)

---

### 9. Search & Discovery

#### Competition Discovery Page
**Filters:**
- Competition type (Coding, Project)
- Status (Upcoming, Active, Judging, Completed)
- Difficulty level
- Tags/categories
- Mode (In-School, Global)
- Date range

**Sorting:**
- Most popular (by participant count)
- Newest first
- Ending soon
- Highest prize pool

**Display:**
- Card-based layout with thumbnail, title, dates, prize, participant count
- "Register" or "View Details" CTA

#### Search Bar
- Search by competition name, tag, or school
- Auto-suggestions as user types

---

### 10. Mobile Responsiveness

**Priority Views:**
- Competition listing (browsing)
- Competition details (reading requirements)
- Submission form (simplified, step-by-step wizard)
- Leaderboard (scrollable table)
- Notifications

**Excluded from MVP:**
- Code editor on mobile (too complex, encourage desktop use)
- Complex judging workflows (judges use desktop)

---

## Technical Architecture

### Technology Stack (Recommended for 3-Day Timeline)

#### Frontend
**Framework:** Next.js 14+ (App Router)
- Server-side rendering for SEO
- API routes for backend logic
- Fast development with hot reload
- Built-in optimization

**UI Library:** Shadcn UI + Tailwind CSS
- Pre-built accessible components
- Customizable design system
- Rapid prototyping
- Clean, modern aesthetic

**Additional Libraries:**
- `react-hook-form` + `zod` for form handling
- `@tanstack/react-query` for data fetching
- `monaco-editor-react` for code editor
- `react-dropzone` for file uploads
- `recharts` for analytics charts
- `date-fns` for date manipulation

#### Backend
**Database:** Supabase (PostgreSQL)
- Real-time subscriptions (for leaderboards)
- Built-in auth with RBAC
- Row-level security (RLS)
- Generous free tier (50,000 monthly active users)
- RESTful API + Postgres functions

**Storage:** Supabase Storage
- File uploads (reports, videos)
- CDN for fast delivery
- Access control via RLS

**Code Execution:** Judge0 API (Free tier)
- 50 requests/day (sufficient for testing)
- Multiple language support
- Sandboxed execution

#### Hosting & Deployment
**Platform:** Vercel (Free tier)
- Automatic deployments from GitHub
- Edge functions for low latency
- 100GB bandwidth/month
- Custom domain support

**CI/CD:** GitHub Actions (if needed)
- Automated testing (future)
- Linting and type checking

#### Email
**Service:** Resend (Free tier: 3,000 emails/month)
- React Email for templates
- High deliverability
- Simple API

#### Analytics (Optional)
**Tool:** Vercel Analytics (Free)
- Page views, user sessions
- No cookie consent needed

---

### System Architecture Diagram

```
┌─────────────────────────────────────────────────────────┐
│                      VERCEL HOSTING                      │
│  ┌───────────────────────────────────────────────────┐  │
│  │           Next.js 14 Application                  │  │
│  │  ┌─────────────┐  ┌─────────────┐  ┌──────────┐  │  │
│  │  │   Pages     │  │  API Routes │  │  Server  │  │  │
│  │  │  (UI/UX)    │  │  (Backend)  │  │  Actions │  │  │
│  │  └─────────────┘  └─────────────┘  └──────────┘  │  │
│  └───────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────┘
                            │
            ┌───────────────┼───────────────┐
            │               │               │
            ▼               ▼               ▼
   ┌─────────────┐  ┌─────────────┐  ┌─────────────┐
   │  SUPABASE   │  │   JUDGE0    │  │   RESEND    │
   │  Database   │  │  Code Exec  │  │    Email    │
   │  + Storage  │  │     API     │  │   Service   │
   └─────────────┘  └─────────────┘  └─────────────┘
```

---

### Database Schema

#### Tables

**1. users**
```sql
id: uuid (PK)
email: varchar (unique)
username: varchar (unique)
full_name: varchar
role: enum ('super_admin', 'facilitator', 'coordinator', 'participant', 'judge')
school_id: uuid (FK → schools, nullable)
country: varchar
profile_picture_url: varchar (nullable)
bio: text (nullable)
date_of_birth: date (nullable, for participants)
grade_level: varchar (nullable, for participants)
skills: text[] (nullable)
points: integer (default 0)
created_at: timestamp
updated_at: timestamp
```

**2. schools**
```sql
id: uuid (PK)
name: varchar
country: varchar
city: varchar
code: varchar (unique, auto-generated)
facilitator_id: uuid (FK → users)
created_at: timestamp
```

**3. competitions**
```sql
id: uuid (PK)
title: varchar
slug: varchar (unique, for URLs)
description: text
banner_image_url: varchar (nullable)
type: enum ('coding', 'project')
mode: enum ('in_school', 'global')
difficulty: enum ('beginner', 'intermediate', 'advanced')
tags: text[]
status: enum ('draft', 'published', 'active', 'judging', 'completed', 'archived')
created_by: uuid (FK → users)
school_id: uuid (FK → schools, nullable, for in-school)
registration_code: varchar (nullable, for in-school)
start_time: timestamp
end_time: timestamp
submission_deadline: timestamp
config: jsonb (stores type-specific settings)
prizes: jsonb (stores prize structure)
rubric: jsonb (stores evaluation criteria)
max_participants: integer (nullable)
created_at: timestamp
updated_at: timestamp
```

**config JSONB structure (examples):**
```json
// Coding competition
{
  "time_limit_minutes": 120,
  "languages": ["python", "javascript", "cpp"],
  "test_cases": [
    {"input": "...", "output": "...", "visible": true},
    {"input": "...", "output": "...", "visible": false}
  ],
  "scoring": {
    "correctness_weight": 0.6,
    "speed_weight": 0.3,
    "quality_weight": 0.1
  }
}

// Project competition
{
  "submission_types": {
    "code_repo": {"required": true},
    "report": {"required": true, "max_size_mb": 10},
    "video": {"required": false, "max_size_mb": 100}
  },
  "allow_teams": true,
  "max_team_size": 3
}
```

**4. registrations**
```sql
id: uuid (PK)
competition_id: uuid (FK → competitions)
user_id: uuid (FK → users)
team_name: varchar (nullable, for team competitions)
team_members: uuid[] (nullable, array of user_ids)
registered_at: timestamp
```

**5. submissions**
```sql
id: uuid (PK)
competition_id: uuid (FK → competitions)
user_id: uuid (FK → users)
team_id: uuid (nullable, references registrations.id for teams)
submission_number: integer (for versioning)
status: enum ('submitted', 'under_review', 'graded')
submitted_at: timestamp

-- For coding competitions
code: text (nullable)
language: varchar (nullable)
execution_time_ms: integer (nullable)
test_results: jsonb (nullable)

-- For project competitions
report_url: varchar (nullable)
repo_url: varchar (nullable)
video_url: varchar (nullable)

-- Scoring
auto_score: float (nullable, for coding)
manual_score: float (nullable)
peer_score: float (nullable)
final_score: float (nullable)
rank: integer (nullable)

created_at: timestamp
updated_at: timestamp
```

**6. reviews**
```sql
id: uuid (PK)
submission_id: uuid (FK → submissions)
reviewer_id: uuid (FK → users)
review_type: enum ('facilitator', 'peer')
rubric_scores: jsonb (key-value pairs for each criterion)
overall_score: float
feedback: text
status: enum ('draft', 'submitted')
created_at: timestamp
updated_at: timestamp
```

**7. notifications**
```sql
id: uuid (PK)
user_id: uuid (FK → users)
type: varchar
title: varchar
message: text
link: varchar (nullable)
read: boolean (default false)
created_at: timestamp
```

**8. badges**
```sql
id: uuid (PK)
name: varchar
description: text
icon_url: varchar
criteria: jsonb
created_at: timestamp
```

**9. user_badges**
```sql
id: uuid (PK)
user_id: uuid (FK → users)
badge_id: uuid (FK → badges)
competition_id: uuid (FK → competitions, nullable)
awarded_at: timestamp
```

**10. discussion_posts**
```sql
id: uuid (PK)
competition_id: uuid (FK → competitions)
user_id: uuid (FK → users)
parent_id: uuid (nullable, for replies, FK → discussion_posts)
content: text
is_announcement: boolean (default false)
upvotes: integer (default 0)
created_at: timestamp
updated_at: timestamp
```

---

### API Endpoints (Key Routes)

#### Authentication
- `POST /api/auth/signup` - Register new user
- `POST /api/auth/login` - Login (handled by Supabase)
- `POST /api/auth/logout` - Logout
- `POST /api/auth/reset-password` - Request password reset

#### Competitions
- `GET /api/competitions` - List competitions (with filters)
- `GET /api/competitions/:id` - Get competition details
- `POST /api/competitions` - Create competition (facilitator only)
- `PATCH /api/competitions/:id` - Update competition
- `DELETE /api/competitions/:id` - Archive competition
- `POST /api/competitions/:id/register` - Register for competition
- `GET /api/competitions/:id/leaderboard` - Get leaderboard

#### Submissions
- `POST /api/submissions` - Create submission
- `GET /api/submissions/:id` - Get submission details
- `PATCH /api/submissions/:id` - Update submission (before deadline)
- `POST /api/submissions/:id/execute` - Run code (coding competitions)

#### Reviews
- `GET /api/reviews/pending` - Get submissions to review (judge)
- `POST /api/reviews` - Submit review
- `PATCH /api/reviews/:id` - Update review

#### Users
- `GET /api/users/profile` - Get current user profile
- `PATCH /api/users/profile` - Update profile
- `GET /api/users/:id/achievements` - Get user badges

#### Analytics (Facilitator)
- `GET /api/competitions/:id/analytics` - Get competition stats

---

### Security Considerations

#### Row-Level Security (RLS) Policies in Supabase

**users table:**
- Users can read their own profile
- Users can update their own profile
- Admins/facilitators can read all profiles

**competitions table:**
- Anyone can read published/active competitions
- Only creators can read draft competitions
- Only creators can update/delete their competitions
- For in-school: only students from that school can see competition

**submissions table:**
- Users can read their own submissions
- Facilitators can read all submissions for their competitions
- Judges can read submissions assigned to them

**reviews table:**
- Reviewers can read/write their own reviews
- Facilitators can read all reviews for their competitions

#### File Upload Security
- Validate file types on client and server
- Scan for malware (use Supabase Storage virus scanning if available)
- Limit file sizes (10MB reports, 100MB videos)
- Generate unique filenames to prevent overwriting

#### Code Execution Security
- Use Judge0 sandboxed environment
- Timeout limits (10 seconds per execution)
- Memory limits (256MB)
- Disable network access for submitted code

#### Anti-Cheating Measures (Basic MVP)
- IP-based rate limiting on submissions
- Track submission times (flag suspiciously fast submissions)
- Code similarity detection (use simple string matching for MVP, future: use tools like MOSS)
- Disable copy-paste in code editor during competition (can be bypassed, but deters casual cheating)

#### GDPR Compliance (Basic)
- Cookie consent banner
- Privacy policy page
- Data export option for users
- Account deletion with data anonymization (not full delete, to preserve competition integrity)

---

## User Flows

### Flow 1: Facilitator Creates a Global Coding Competition

1. Facilitator logs in
2. Navigates to Dashboard → "Create Competition"
3. Selects "Coding Competition"
4. Selects "Global" mode
5. Fills form:
   - Title: "Winter Algorithms Challenge 2026"
   - Description: Rich text with problem statement
   - Difficulty: Intermediate
   - Tags: Algorithms, Dynamic Programming
   - Start: Jan 15, 2026 10:00 AM
   - End: Jan 15, 2026 12:00 PM
   - Languages: Python, C++, JavaScript
6. Adds test cases (3 visible, 5 hidden)
7. Sets prizes: 1st ($500), 2nd ($300), 3rd ($100)
8. Previews competition page
9. Publishes competition
10. Competition appears on homepage "Upcoming Competitions"

### Flow 2: Student Registers and Submits for Coding Competition

1. Student browses homepage, sees "Winter Algorithms Challenge 2026"
2. Clicks "View Details"
3. Reads problem statement
4. Clicks "Register Now"
5. If not logged in, prompted to sign up/log in
6. After registration, redirected to competition page
7. When competition starts, "Start Competing" button activates
8. Student clicks button, timer starts
9. Reads problem, writes code in Monaco editor
10. Clicks "Run Code" to test with sample inputs
11. Reviews output
12. Clicks "Submit Solution"
13. Code sent to Judge0 API for evaluation
14. Real-time feedback: "5/8 test cases passed"
15. Student refines code, submits again
16. All test cases pass
17. Leaderboard updates with student's rank (based on time)
18. Student receives confirmation email

### Flow 3: Facilitator Creates In-School Project Competition

1. Facilitator logs in
2. Navigates to Dashboard → "Create Competition"
3. Selects "Project Competition"
4. Selects "In-School" mode
5. Selects school from dropdown (or creates new school)
6. Fills form:
   - Title: "Robotics Innovation Challenge"
   - Description: Build a robot to solve X problem
   - Deadline: Feb 1, 2026 11:59 PM
   - Submission types: Code repo (required), Video (required), Report (optional)
   - Team size: 2-3 members
7. Defines rubric:
   - Innovation (30 points)
   - Technical Implementation (40 points)
   - Presentation (30 points)
8. Sets prizes: Certificates + badges
9. Publishes competition
10. System generates school code: `ROBOT-MAPLE-2026`
11. Facilitator shares code with school coordinator
12. School coordinator shares code with students

### Flow 4: Student Submits Project

1. Student logs in, enters school code `ROBOT-MAPLE-2026`
2. Joined school-specific competition
3. Forms team (invites 2 other students by email)
4. Teammates accept invitations
5. As deadline approaches, team prepares submission
6. Team lead navigates to competition → "Submit Project"
7. Fills submission form:
   - Uploads report PDF (drag-and-drop)
   - Pastes GitHub repo link
   - Pastes YouTube video link
8. Previews submission
9. Clicks "Submit"
10. Receives confirmation: "Submission #1 received at 2026-02-01 10:45 PM"
11. Realizes they forgot to add README to repo
12. Updates repo, returns to platform
13. Clicks "Resubmit" (allowed before deadline)
14. Submits v2
15. Email confirmation sent to all team members

### Flow 5: Facilitator and Peer Review Workflow

1. Submission deadline passes
2. Competition status changes to "Judging"
3. Facilitator receives email: "15 submissions ready for review"
4. Facilitator logs in → Judging Dashboard
5. Sees list of submissions
6. Clicks on Submission #1
7. Views report PDF, watches video, browses code repo
8. Fills rubric:
   - Innovation: 25/30 ("Great concept but similar to existing projects")
   - Implementation: 35/40 ("Solid code, minor bugs")
   - Presentation: 28/30 ("Clear video, excellent narration")
9. Total: 88/100
10. Writes overall feedback: "Well executed project! Consider..."
11. Clicks "Submit Review"
12. Moves to next submission

(Parallel process for peer review, if enabled:)

1. Participant A finishes their submission
2. System assigns Participant A to review 2 peer submissions (from different schools to avoid conflicts)
3. Participant A receives email: "You've been selected as a peer reviewer"
4. Logs in → Peer Review Dashboard
5. Sees simplified rubric (3 criteria instead of full rubric)
6. Reviews 2 submissions, provides constructive feedback
7. Submits reviews
8. Peer scores weighted at 20% of final score

### Flow 6: Results Publication

1. All reviews completed
2. Facilitator logs in → Competition Dashboard
3. Clicks "Finalize Results"
4. System calculates final scores (80% facilitator + 20% peer average)
5. Ranks submissions
6. Facilitator reviews rankings, can manually adjust if needed
7. Clicks "Publish Results"
8. Competition status changes to "Completed"
9. All participants receive email: "Results are out!"
10. Leaderboard published on competition page
11. Winners see badges added to profiles
12. Certificates auto-generated with winner names
13. Winners can download certificates from profile

---

## UI/UX Requirements

### Design Principles
1. **Clarity over creativity:** Competition rules and deadlines must be immediately obvious
2. **Minimal friction:** 3 clicks max from homepage to competition registration
3. **Trust signals:** Show participant counts, past winners, XploreSTEMi branding
4. **Accessibility:** WCAG 2.1 AA compliance (color contrast, keyboard navigation, alt text)
5. **Mobile-first:** 60% of students will browse on phones

### Design System

#### Colors
- **Primary:** #2563EB (Blue) - CTAs, links
- **Secondary:** #10B981 (Green) - Success states, badges
- **Accent:** #F59E0B (Amber) - Warnings, featured competitions
- **Danger:** #EF4444 (Red) - Errors, deadlines
- **Neutral:** Grays (#F9FAFB to #111827) for backgrounds, text

#### Typography
- **Headings:** Inter font, bold (600-700)
- **Body:** Inter font, regular (400)
- **Code:** JetBrains Mono (for code snippets)

#### Components (via Shadcn UI)
- Buttons (primary, secondary, ghost, danger)
- Cards (for competition listings)
- Modals (for confirmations)
- Forms (inputs, selects, textareas with validation states)
- Tabs (for switching views)
- Toast notifications (for feedback)
- Progress bars (for file uploads, time remaining)

### Key Screens (Wireframe Descriptions)

#### 1. Homepage
**Layout:**
- Hero section: "Compete. Learn. Win." + CTA ("Browse Competitions")
- Featured global competitions (carousel, 3 cards)
- Upcoming competitions (grid, 6 cards)
- Past winners spotlight (3 profiles with badges)
- Stats: X students, Y competitions, Z prizes awarded
- Footer: Links, social media, XploreSTEMi logo

**Responsive:**
- Mobile: Single column, hero shorter
- Desktop: 3-column grid for competitions

#### 2. Competition Listing Page
**Layout:**
- Search bar + filters sidebar (left)
- Competition cards grid (right, 3 columns)
- Pagination at bottom

**Card Content:**
- Banner image (16:9)
- Title + difficulty badge
- Tags (max 3 visible)
- Start date + duration
- Prize amount (if any)
- Participant count + "XX spots left" if capped
- "Register" or "View Details" button

#### 3. Competition Detail Page
**Layout:**
- Banner image (full-width)
- Title + breadcrumb (Home > Competitions > [Title])
- Key info bar: Start date, End date, Difficulty, Mode (in-school/global)
- Tabs:
  - Overview (description, rules, prizes)
  - Problem Statement (for coding) / Requirements (for projects)
  - Submissions (if user registered, shows submission form/status)
  - Leaderboard (if active/completed)
  - Discussion (Q&A forum)
- Right sidebar:
  - Registration status ("Registered!" or "Register Now" button)
  - Countdown timer (if active)
  - Prize breakdown
  - Organizer info (facilitator profile)

**For Coding Competitions:**
- Problem tab includes: Description, constraints, examples, test cases (visible ones)

**For Project Competitions:**
- Requirements tab includes: Submission types checklist, rubric table, resource links

#### 4. Submission Page (Coding)
**Layout:**
- Split screen:
  - Left: Problem statement (collapsible)
  - Right: Code editor (Monaco)
- Top bar: Timer, language selector, "Run Code" and "Submit" buttons
- Bottom: Console output (test results, errors)

**Features:**
- Syntax highlighting
- Auto-indentation
- Keyboard shortcuts (Ctrl+S to save locally)

#### 5. Submission Page (Project)
**Layout:**
- Stepper: Step 1 (Code Repo) → Step 2 (Report) → Step 3 (Video) → Review
- Each step: Instructions + input field/upload zone
- Progress indicator (e.g., "2 of 3 required submissions complete")
- "Save Draft" and "Submit" buttons

**Validation:**
- Real-time: "Report must be PDF or DOCX, max 10MB" error if wrong type
- Green checkmarks when each step validated

#### 6. Facilitator Dashboard
**Layout:**
- Sidebar navigation: Competitions, Analytics, Judging, Settings
- Main area:
  - Summary cards: Active competitions (X), Pending reviews (Y), Total participants (Z)
  - Recent activity feed
  - Quick actions: "Create Competition", "View Reports"

**Competitions Tab:**
- Table: Title, Type, Mode, Status, Participants, Actions (Edit, View, Archive)
- Filters: Status, Type, Date range

**Judging Tab:**
- List of submissions awaiting review
- Sort by: Submission date, Score (if partial reviews done)
- Click submission → Review modal opens

#### 7. Leaderboard Page
**Layout:**
- Podium graphic for Top 3 (large profile pics + scores)
- Table below: Rank, Username, School, Score, Time/Submission Date
- Filters: School (for in-school), Country (for global)
- Pagination (20 per page)
- User's rank highlighted if not in top 20

**Export:**
- "Download as CSV" button (facilitator only)

#### 8. User Profile Page
**Layout:**
- Profile header: Picture, Name, School, Country, Bio
- Tabs:
  - Overview: Points, Badges, Competition history (list)
  - Achievements: Badge showcase (grid)
  - Statistics: Competitions entered, Win rate, Avg score

**Privacy:**
- Users can set profile to private (only visible to facilitators)

---

### Responsive Breakpoints
- Mobile: < 640px (single column, stacked layouts)
- Tablet: 640px - 1024px (2 columns where applicable)
- Desktop: > 1024px (3 columns, full sidebars)

---

## Security & Permissions

### Role-Based Permissions Matrix

| Action | Super Admin | Facilitator | Coordinator | Participant | Judge |
|--------|-------------|-------------|-------------|-------------|-------|
| Create competition | ✅ | ✅ (own schools only) | ❌ | ❌ | ❌ |
| Edit competition | ✅ | ✅ (own only) | ❌ | ❌ | ❌ |
| Delete competition | ✅ | ✅ (own only) | ❌ | ❌ | ❌ |
| View all users | ✅ | ✅ (own schools) | ✅ (own school) | ❌ | ❌ |
| Register for competition | ❌ | ❌ | ✅ | ✅ | ✅ |
| Submit to competition | ❌ | ❌ | ✅ | ✅ | ❌ |
| Review submissions | ✅ | ✅ (own competitions) | ❌ | ✅ (peer review) | ✅ |
| Publish results | ✅ | ✅ (own only) | ❌ | ❌ | ❌ |
| View analytics | ✅ | ✅ (own competitions) | ✅ (own school) | ❌ | ❌ |

### Data Privacy
- Students under 18: Require parental consent (checkbox during signup)
- No public display of full names without user consent (use username option)
- Email addresses never shown publicly
- Allow users to export their data (GDPR compliance)
- Allow users to delete accounts (anonymize data, don't fully delete to preserve competition history)

---

## Development Roadmap (3-Day Sprint)

### Day 1: Foundation & Core Features
**Hours 1-3: Project Setup**
- Initialize Next.js project with TypeScript
- Set up Shadcn UI and Tailwind
- Connect Supabase (database + auth)
- Create GitHub repo + Vercel project
- Set up environment variables

**Hours 4-8: Authentication & User Management**
- Implement signup/login (email + Google OAuth)
- Create user profile pages
- Build role selection during signup
- Set up RLS policies for users table

**Hours 9-12: Competition Creation (Facilitator)**
- Build competition creation form (multi-step)
- Store competitions in database
- Implement draft/publish flow
- Create competition listing page (public)

**Day 1 Deliverable:** Facilitators can create and publish competitions; users can sign up and view competitions.

---

### Day 2: Competition Participation & Submissions
**Hours 1-4: Registration System**
- Build registration flow for students
- Generate school codes for in-school competitions
- Create "My Competitions" dashboard for students

**Hours 5-8: Submission System (Coding)**
- Integrate Monaco code editor
- Connect Judge0 API for code execution
- Implement test case validation
- Store submissions in database

**Hours 9-12: Submission System (Projects)**
- Build multi-step submission form (file uploads + links)
- Integrate Supabase Storage for file uploads
- Implement submission versioning (allow resubmit)
- Create submission confirmation page

**Day 2 Deliverable:** Students can register, submit code solutions, and upload project files. Code execution works.

---

### Day 3: Judging, Results & Polish
**Hours 1-4: Judging System**
- Build judge dashboard (list of submissions)
- Create review form with rubric scoring
- Implement peer review assignment (if time permits, otherwise skip for MVP)
- Calculate final scores (weighted averages)

**Hours 5-8: Leaderboard & Results**
- Build real-time leaderboard for coding competitions
- Create results page with podium graphic
- Generate winner certificates (PDF export)
- Implement badge awarding system

**Hours 9-10: Notifications & Communication**
- Set up email notifications (Resend integration)
- Implement in-app notification system (basic)
- Add discussion forum per competition (basic Q&A)

**Hours 11-12: Testing & Deployment**
- End-to-end testing of key flows
- Fix critical bugs
- Deploy to Vercel
- Set up custom domain (if available)

**Day 3 Deliverable:** Fully functional MVP with judging, results, and notifications. Platform is live.

---

### Post-Launch (Days 4-7): Iteration Based on Feedback
- User testing with small group (10-20 students)
- Fix bugs reported
- Add missing features based on priority
- Optimize performance (lazy loading, caching)

---

## Success Metrics

### Launch Metrics (Week 1)
- [ ] 50+ users registered
- [ ] 5+ competitions created
- [ ] 100+ submissions received
- [ ] 90%+ submission success rate (no failed uploads)
- [ ] <2 seconds page load time
- [ ] 0 critical bugs reported

### Growth Metrics (Month 1)
- [ ] 500+ users registered
- [ ] 10+ schools participating in in-school competitions
- [ ] 20+ global competitions completed
- [ ] 50%+ user retention (users return for 2nd competition)
- [ ] 4.5+ average user satisfaction rating (via post-competition survey)

### Engagement Metrics
- Average time per session: >10 minutes
- Competitions per user: >2
- Submission rate (registered vs submitted): >70%
- Discussion posts per competition: >15

### Operational Metrics
- Competition creation time: <5 minutes (facilitator feedback)
- Judging time per submission: <10 minutes (facilitator feedback)
- Support tickets per 100 users: <5

---

## Future Enhancements (Post-MVP)

### Phase 2 (Months 2-3)
- **Team management:** Advanced team formation (auto-matching by skills)
- **Live streaming:** Host live kickoff events or award ceremonies
- **Mobile app:** Native iOS/Android app for better mobile experience
- **Advanced anti-cheating:** Code plagiarism detection using AI
- **Gamification:** Levels, streaks, daily challenges
- **Sponsor portal:** Allow sponsors to fund prizes and get branded pages

### Phase 3 (Months 4-6)
- **Mentorship program:** Connect students with mentors during competitions
- **Video interviews:** Record short video intros from participants (optional)
- **Multi-language support:** Interface in French, Swahili, etc.
- **AI-assisted judging:** Use LLMs to provide initial feedback on reports
- **API for partners:** Allow other orgs to host competitions on XploreSTEMi platform

### Phase 4 (Months 7-12)
- **Career portal:** Job board for competition winners
- **Virtual reality:** VR experiences for robotics competitions
- **Blockchain badges:** NFT certificates for winners
- **AI content generation:** Auto-generate problem sets using LLMs

---

## Risk Assessment & Mitigation

### Technical Risks

**Risk 1: Judge0 API rate limits (50 requests/day on free tier)**
- **Impact:** Can't test more than 50 code submissions per day
- **Mitigation:** 
  - Upgrade to Judge0 paid plan ($5/month, 200 requests/day) if needed
  - Alternative: Self-host Judge0 (requires Docker, more complex)
  - For testing: Limit test competitions to 10 participants

**Risk 2: Supabase storage limits (1GB on free tier)**
- **Impact:** Can't store many large video files
- **Mitigation:**
  - Encourage YouTube/Vimeo links over uploads
  - Compress videos before upload (client-side)
  - Upgrade to Supabase Pro ($25/month, 100GB) when needed

**Risk 3: Vercel bandwidth limits (100GB/month free)**
- **Impact:** Site goes down if traffic spikes
- **Mitigation:**
  - Optimize images (use Next.js Image component)
  - Use Supabase CDN for file delivery
  - Monitor usage dashboard
  - Upgrade to Vercel Pro ($20/month, 1TB) if needed

### Product Risks

**Risk 4: Low user adoption (students don't find competitions appealing)**
- **Mitigation:**
  - Launch with 2-3 "pilot" competitions with guaranteed prizes
  - Partner with schools to mandate participation for XploreSTEMi clubs
  - Collect feedback via surveys after each competition

**Risk 5: Facilitators struggle to create competitions (too complex)**
- **Mitigation:**
  - Provide competition templates (presets for common formats)
  - Video tutorials on competition creation
  - 1-on-1 onboarding calls with first-time facilitators

**Risk 6: Cheating/plagiarism undermines competition integrity**
- **Mitigation:**
  - Start with honor code system (students sign agreement)
  - Implement basic anti-cheating (IP tracking, time analysis)
  - Post-MVP: Add AI-powered plagiarism detection
  - For critical competitions: Require proctored sessions (via Zoom, facilitator monitors)

### Operational Risks

**Risk 7: Support burden (students need help with tech issues)**
- **Mitigation:**
  - Comprehensive FAQ page
  - Video walkthroughs for common tasks
  - Dedicated support email (route to volunteer team)
  - In-app chat widget (use Tawk.to free tier)

**Risk 8: Scalability issues (platform crashes during large competition)**
- **Mitigation:**
  - Load testing before major launches (use tools like k6)
  - Set max participant caps for first few competitions
  - Monitor server metrics (Vercel Analytics)
  - Have backup plan (postpone competition if site down)

---

## Appendix

### A. Glossary
- **Competition:** An event where students solve challenges to win prizes
- **Facilitator:** XploreSTEMi team member who creates and manages competitions
- **Coordinator:** Student leader at a school club
- **Participant:** Student competing
- **Judge:** Person evaluating submissions (facilitator or peer)
- **Submission:** A participant's solution to a competition challenge
- **Rubric:** Scoring criteria for evaluating submissions
- **Leaderboard:** Ranked list of participants by score
- **Badge:** Digital achievement displayed on user profile

### B. User Research Insights (Assumptions for MVP)
- **Students prefer mobile browsing** but **submit from desktop** (esp. for coding)
- **Video demos are most engaging** submission type (based on XploreSTEMi bootcamp feedback)
- **Prizes are strong motivator**, but **recognition (badges, certificates) also valued**
- **Clear deadlines and rules reduce support tickets**
- **Real-time leaderboards increase excitement** during coding competitions

### C. Competitor Analysis (Platforms with Similar Features)
- **HackerRank:** Strong code execution, but expensive and not non-profit friendly
- **Kaggle:** Great for data science, but too advanced for high schoolers
- **DevPost:** Good for hackathons, but lacks in-school segmentation
- **Codewars:** Gamified coding practice, but no project submissions
- **XploreSTEMi Advantage:** Dual-mode (in-school + global), project competitions, non-profit focus, STEM education alignment

### D. Open Questions (to Revisit Post-Launch)
1. Should we allow team competitions for coding challenges? (MVP: solo only)
2. Do we need a mobile app, or is responsive web enough? (MVP: web only)
3. How to handle disputes (e.g., student claims unfair judging)? (MVP: facilitator has final say)
4. Should peer reviews be anonymous? (MVP: yes)
5. How to incentivize peer reviewers to give quality feedback? (MVP: badge for "Helpful Reviewer")

### E. Contact Information
- **Product Owner:** Joshua (joshua@xplorestemi.org)
- **Tech Support:** (TBD, volunteer team)
- **Feedback:** feedback@xplorestemi.org

---

## Approval & Sign-Off

**Prepared By:** Joshua (XploreSTEMi Engineering Team Lead)  
**Date:** January 8, 2026  
**Version:** 1.0  

**Next Steps:**
1. Review PRD with XploreSTEMi core team
2. Finalize tech stack and hosting budget
3. Kick off Day 1 development
4. Schedule daily check-ins during 3-day sprint

---

_This PRD is a living document and will be updated as the product evolves._
