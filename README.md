# NELC-Integration
# NELC — xAPI Profiles Guidelines  
**Version 02 — 6-9-2022**  
**NELC — Digital Transformation Department**

---

## Table of Contents
- [Overview](#overview)
- [Concepts, Verbs and Activity](#concepts-verbs-and-activity)
- [Guidelines](#guidelines)
- [Learner Engagement Scenario](#learner-engagement-scenario)
- [Sample Statements](#sample-statements)
- [Notes to Consider and Common Mistakes](#notes-to-consider-and-common-mistakes)
- [Resources](#resources)
- [Contact Us](#contact-us)

---

## Overview
This file explains how to seamlessly integrate an Education Provider with FutureX through xAPI.  
It describes how to author an xAPI Profile using JSON-based semantic triples (subject–predicate–object).

---

## Concepts, Verbs and Activity

### Table 1: Concepts, Verbs and Activity

| Concept Name | Description | Concept Type | IRI |
|--------------|-------------|--------------|-----|
| registered | Indicates the actor is officially enrolled or inducted in an activity. | Verb | http://adlnet.gov/expapi/verbs/registered |
| initialized | Indicates the actor successfully started an activity. | Verb | http://adlnet.gov/expapi/verbs/initialized |
| watched | Actor watched dynamic content; more specific than *experience* or *consume*. | Verb | https://w3id.org/xapi/acrossx/verbs/watched |
| completed | Actor finished the activity normally. | Verb | http://adlnet.gov/expapi/verbs/completed |
| attended | Actor was present at a virtual or physical activity. | Verb | http://adlnet.gov/expapi/verbs/attended |
| progressed | Indicates how much the actor advanced in an activity. | Verb | http://adlnet.gov/expapi/verbs/progressed |
| rated | Actor rated an object. Rating should be in Result.Score. | Verb | http://id.tincanapi.com/verb/rated |
| earned | Actor earned or was awarded the object. | Verb | http://id.tincanapi.com/verb/earned |
| attempted | Actor attempted to access the object. | Verb | http://adlnet.gov/expapi/verbs/attempted |
| attempt-id | Distinguishes between attempts. | Extension | http://id.tincanapi.com/extension/attempt-id |
| browser information | Browser metadata (same as user-agent). | Extension | http://id.tincanapi.com/extension/browser-info |
| jws certificate location | URL of public certificate to verify signature. | Extension | http://id.tincanapi.com/extension/jws-certificate-location |
| unit test | A unit test inside a software project. | ActivityType | http://id.tincanapi.com/activitytype/unit-test |
| lesson | Learning content that may be standalone or course-related. | ActivityType | http://adlnet.gov/expapi/activities/lesson |
| course | Learning content published with a completion goal. | ActivityType | https://w3id.org/xapi/cmi5/activitytype/course |
| video | Recording of visual and audio content. | ActivityType | https://w3id.org/xapi/video/activity-type/video |
| module | Content aggregation level below course. | ActivityType | http://adlnet.gov/expapi/activities/module |
| certificate | Proof a user completed a course. | ActivityType | https://www.opigno.org/en/tincan_registry/activity_type/certificate |
| assessment | Generic competence assessment. | ActivityType | https://w3id.org/xapi/tla/activity-types/assessment |
| school assignment | Student task. | ActivityType | http://id.tincanapi.com/activitytype/school-assignment |
| virtual classroom | Online live classroom session. | ActivityType | https://w3id.org/xapi/virtual-classroom/activity-types/virtual-classroom |
| LMS URL | Learning platform URL. | Extension | https://nelc.gov.sa/extensions/lms_url |
| program URL | Program/course URL. | Extension | https://nelc.gov.sa/extensions/program_url |

---

## Guidelines
- LMS must send minimum learner activity events needed to measure progress.
- Backend authentication is mandatory — frontend authentication not accepted.
- NELC provides endpoint credentials upon formal request.
- Course completion types:
  - Passing unit quiz
  - Passing final course exam
  - Watching course videos (90% consumption = watched)
- "actor.name" **must be learner’s unique ID** (National ID, Iqama, etc.).
- Course **description must be full and clean (no HTML)** in the registration statement.
- Durations must follow **ISO 8601**: `PT1H22M17S`.
- Timestamp format: `2022-01-31T07:18:32.829Z`.
- **Platform format:** PROV-NUM (e.g., GELS-001).
- Language must use **ISO 639-1** codes (e.g., `ar-SA`, `en-US`).
- Certificate link must be inside:  
  `http://id.tincanapi.com/extension/jws-certificate-location`
- Videos are considered watched when 90% of duration is consumed.
- Progress can be explicitly sent using the **progressed** verb.

---

## Learner Engagement Scenario

### Table 2: Learner Engagement Scenario

(A full table is preserved in your file. GitHub renders wide tables horizontally — still readable.)

---

## Sample Statements

All JSON statements are converted into valid Markdown fenced code blocks:

### Statement #1 — **registered**
```json
{
  "actor": {
    "mbox": "mailto:1234567890@gmail.com",
    "name": "1234567890",
    "objectType": "Agent"
  },
  "verb": {
    "id": "http://adlnet.gov/expapi/verbs/registered",
    "display": {"en-US": "registered"}
  },
  ...
}

```
### Statement #2 — **initialized**
```json
{
  "actor": {
    "mbox": "mailto:1234567890@gmail.com",
    "name": "1234567890",
    "objectType": "Agent"
  },
  ...
}
```
