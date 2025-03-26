## Event Storming
### Event Storming Legend
![Event Storming Legend](../images/event-storming/00-event-storming-legend.png)
### Event Identification
![Event Identification](../images/event-storming/01-event-identification.png)
### Command, Event and Actor Identification
![Command, Event and Actor Identification](../images/event-storming/03-aggregate-identification.png)
### Ubiqueous Language
![Ubiquiteous Language](../images/event-storming/04-ubiquiteous-language.png)
### Overall Flow
![Overall Flow](../images/event-storming/05-overall-flow.png)
### Flows
After event storming we have narrowed down on the different business flows

| Business Flow | Commands | Events | Policies |
| ----- | ----- | ----- | ----- |
| ﻿Starting interview  | <ul><li>﻿Create Interview Process</li><li>﻿Start Round</li></ul> | <ul><li>Interview Process Created</li><li>Round Started</li></ul> | <ul><li>Consult Interview Plan</li><li>Consult round plan</li></ul><p></p> |
| ﻿Interviewers Matching  | <ul><li>﻿Store Interviewer Profiles</li><li>﻿Store Interviewer Availability</li><li>﻿Store Interviewer Leave Plan</li><li>﻿Fetch Interviewer Availability</li><li>﻿Fetch Interviewer Leave Plan</li><li>﻿Fetch Interviewer Profiles</li><li>﻿Match Interviewers To Criteria</li><li>﻿Assign Interviewers</li></ul> | <ul><li>Interviewer Profiles Fetched</li><li>Interviewers Profiles Stored</li><li>Interviewers Availability Stored</li><li>Interviewers Leave Plan Stored</li><li>Interviewer Availability Fetched</li><li>Interviewer Leave Plan Fetched</li><li>Interviewers Matched</li><li>Interviewers Assigned</li></ul> | <ul><li>Match on participants skills & profile</li><li>Meets required interviewers criteria and availability</li></ul> |
| ﻿Scheduling Interview Round  | <ul><li>﻿Schedule round</li><li>﻿Notify Round Participants</li><li>﻿Interviewee Accept  Invite</li><li>﻿Interviewer Accept Invite</li><li>﻿Mark Round As Confirmed</li></ul> | <ul><li>Round Scheduled</li><li>Interviewee Notified</li><li>Interviewers Notified</li><li>All Participants Accepted</li><li>Round Confirmed</li></ul> | <ul><li>Required Participants Selected</li><li>All participants have accepted invite</li></ul> |
| ﻿Reschedule Round  | <ul><li>﻿Interviewer Reject Invite</li><li>﻿Interviewee Reject Invite</li><li>﻿Update Round Criteria</li></ul> | <ul><li>Interviewer Invite Rejected</li><li>Interviewee Invite Rejected</li><li>Round Criteria Updated</li></ul> | <ul><li>One or more participant have rejected invite</li></ul> |
| ﻿Interview Process  | <ul><li>﻿Mark round in progress</li><li>﻿Submit Score card</li><li>﻿Mark round As Complete</li><li>﻿Hire Interviewee</li><li>﻿Don't hire Interviewee</li><li>﻿Mark Interview As Complete</li><li>﻿Mark Interview On Hold</li><li>﻿Mark Interview Cancelled</li></ul> | <ul><li>Round In Progress</li><li>Score card submitted</li><li>Round Completed</li><li>Interview Completed</li><li>Interviewee Hired</li><li>Interviewee Not Hired</li><li>Interview On Hold</li><li>Interview Cancelled</li></ul> | <ul><li>No change in participants decision</li><li>All rounds completed</li><li>Provide reason for holding interview</li><li>Provide reason for cancellation</li></ul> |
| ﻿Round Not Confirmed  | <ul><li>﻿Round Confirmation Timeout</li></ul> | <ul><li>Round Not confirmed On Time</li></ul> | <ul><li>Round Confirmation Policy Violated</li></ul> |
| ﻿Manually Assign Interviewers  | <ul><li>﻿Manually select Interviewers</li></ul> | <ul><li>Interviewers Selected</li></ul> | <ul><li>Provide reason for manual selection</li></ul> |
#### 1. Starting Interview
![Starting Interview](../images/event-storming/flows/01-starting-interview-flow.png)

#### 2. Interviewer Matching
![Interviewer Matching](../images/event-storming/flows/02-interviewer-matching-flow.png)

#### 3. Interview Scheduling
![Interview Scheduling](../images/event-storming/flows/03-scheduling-interview-round-flow.png)

#### 4. Interview Rescheduling
![Interview Rescheduling](../images/event-storming/flows/04-rescheduling-and-manual-selection-flow.png)

#### 5. Interview Process
![Interview Process](../images/event-storming/flows/05-interview-process-flow.png)
