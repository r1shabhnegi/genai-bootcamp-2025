# Frontend Technical Specs

## Pages

### Dashboard '/dashboard'

#### Purpose

The purpose of this page is to provide a summary of learning and act as the default page when a user visits the webpage

#### components

- Last study session
  - shows last activity used
  - shows when last activity used
  - summarizes wrong vs correct from last activity
  - has a link to the group
- Study progress
  - total words studied eg. 3/124
    - across all study sessions show the total words studied out of all possible words in our database
  - display a mastery progress eg. 0%
- Quick stats
  - success rate eg. 80%
  - total study session eg. 4
  - total active groups eg. 3
  - study streak eg. 4 days
- Start studying Button
  - goes to study activities page

#### Needed API Endpoints

- GET /api/dashboard/last_study_session
- GET /api/dashboard/study_progress
- GET /api/dashboard/quick-stats

### Study activities Index '/study-activities'

#### Purpose

The purpose of this page is to show a collection of study activities with a thumbnail and its name, to either launch or view the study activity.

#### components

- Study Activity Card
  - show a thumbnail of the study activity
  - The name of the study activity
  - a launch button to take us to the launch page
  - the view page to view more information about past study session for this study activity

#### Needed API Endpoints

- GET /api/study_activities

---

### Study Activity Show '/study-activities/:id'

#### Purpose

The purpose of this page is to show the details of a study activity and its past study sessions

#### components

- Name of study activity
- Thumbnail of study activities
- Description of study activity
- Launch button
- Study activities paginated list
  - id
  - activity
  - group name
  - start time
  - end time (inferred by the last word_review_item submitted)
  - number of review items

#### Needed API Endpoints

- GET /api/study_activities/:id
- GET /api/study_activities/:id/study_sessions

### Study Activities Launch '/study_activities/:id/launch'

#### Purpose

The purpose of this page is to launch a study activity

#### components

- Name of study activity
- Launch form
  - select field for group
  - launch now button

## Behaviour

After the form is submitted a new tab opens with the study activity based on its URL provided in the database.

Also the after form is submitted the page will redirect to the study session show page.

#### Needed API Endpoints

- POST /api/study_activities

### Words Index '/words'

#### Purpose

The purpose of this page is to show all words in our database.

#### components

- Paginated word list
  - columns
    - Japanese
    - romaji
    - english
    - correct count
    - wrong count
  - Pagination with 100 items per page
  - clicking the japanese word will take us to the word show page

#### Needed API Endpoints

- GET /api/words

### Word Show '/words/:id'

#### Purpose

The purpose of this page is to show information about a specific word.

#### components

- Japanese
- Romaji
- English
- Study statistics
  - correct count
  - wrong count
- word groups
  - show an a series of pills eg. tags
  - When group name is clicked it will take us to the group show page

#### Needed API Endpoints

- GET /api/words/:id

### Word Groups Index '/groups'

#### Purpose

The purpose of this page is to show a list of groups in out database

#### components

- paginated group list
  - columns
    - group name
    - word count
  - Clicking the group name will take us to the group show page

#### Needed API Endpoints

- GET /api/groups

### Group Show '/groups/:id'

#### Purpose

The purpose of this page is to show information about a specific group

#### components

- Group Name
- Group Statistics
  - total word count
- words in group (paginated list o words)
  - should use the same component as the words index page
- study sessions (paginated list of study sessions)
  - should use the same component as the study sessions index page

#### Needed API Endpoints

- GET /api/groups/:id (the name and groups statistics)
- GET /api/groups/:id/words
- GET /api/groups/:id/study_sessions

### Study Sessions Index '/study-sessions'

#### Purpose

The purpose of this page is to show a list of study sessions in our database.

#### components

- Paginated study session list
  - columns
    - id
    - activity name
    - group name
    - start time
    - end time
    - number of review items
  - clicking the study session id will take us to the study session show page

#### Needed API Endpoints

- GET /api/study_sessions

### Study Session Show '/study-sessions/:id'

#### Purpose

The purpose of this page is to show information about a specific study session.

#### components

- Study session details
  - activity name
  - group name
  - start time
  - end time
  - number of review items
- word review items (paginated list of words)
  - should use the same component as the words index page

#### Needed API Endpoints

- GET /api/study_sessions/:id
- GET /api/study_sessions/:id/words

### Settings Page '/settings'

#### Purpose

The purpose of this is to make configurable to the study portal.

#### components

- Theme selection eg. light, dark, system default
- reset history button
  - this will delete all study session and word review items
- Full reset button
  - this will drop all table and re-create with seed data

#### Needed API Endpoints

- POST /api/settings/reset_history
- POST /api/settings/full_reset
