# Backend Server Technical Specs

## Business Goal:

A language learning school wants to build a prototype of learning portal which will act as three things:

- Inventory of possible vocabulary that can be learned
- Act as a Learning record store (LRS), providing correct and wrong score on practice vocabulary
- A unified launchpad to launch different learning apps

## Technical Requirements

- The backend will be build using node.js.
- The database will be SQLite3.
- The API will be build using ExpresJS
- The API will always return JSON
- There will be no authentication or authorization
- Everything will be treated as a single user

## Database Schema

We have the following tables:

- words - stored vocabulary words
  - id integer
  - japanese string
  - rajami string
  - english string
  - parts json
- words_groups - join table for words and groups many to many
  - id integer
  - word_id integer
  - group_id integer
- groups - thematic groups of words
  - id integer
  - name string
- study sections - records of study sessions grouping word_review_items
  - id integer
  - group_id integer
  - created_at datatime
  - study_activity_id integer
- study_activities - a specific study activity, linking a study session to a group
  - id integer
  - study_session_id integer
  - group_id integer
  - created_at datatime
- word_review_items - a record of word practice, determining if the word was correct or not
  - word_id integer
  - study_session_id integer
  - correct boolean
  - created_at datatime

### API Endpoints

- GET /api/dashboard/last_study_session
- GET /api/dashboard/study_progess
- GET /api/dashboard/quick-stats
- GET /api/study_activities/:id
- GET /api/study_activities/:id/study_sessions
- POST /api/study_activities
  - required params: group_id, study_activity_id
- GET /api/words
  - pagination with 100 items per page
- GET /api/words/:id
- GET /api/groups
  - pagination with 100 items per page
- GET /api/groups/:id
- GET /api/groups/:id/words
- GET /api/groups/:id/study_sessions
- GET /api/study_sessions
  - pagination with 100 items per page
- GET /api/study_sessions/:id
- GET /api/study_sessions/:id/words
- POST /api/settings/reset_history
- POST /api/settings/full_reset
- POST /api/study_sessions/:id/words/:word_id/review
  - required params: correct
