# 1. Blackboard Ultra → xAPI Mapping Dictionary

Complete, hierarchical, ready for implementation.

## 1.1 Institution / Organization Metadata

(Extractable via Blackboard REST APIs, SIS Integration APIs, and Ultra “Institutional Hierarchy”)

| Blackboard Entity | API Source | xAPI Object Type | Required Data | Notes |
|------------------|------------|------------------|----------------|-------|
| University | Institutional Hierarchy | Group | org:id, name, code | You will define each tenant/university as an xAPI “group” |
| College / Faculty | Institutional Hierarchy | Group | college_id, name | Optional: hierarchy path |
| Department | Institutional Hierarchy | Group | dept_id, name | |
| Program | Institutional Hierarchy or course module metadata | Group | program_id, name | Depends on institution; some use metadata in courses |
| Semester / Term | Term API | Activity | term_id, title, start_date, end_date | Blackboard populates "terms" out of the box |
| Cluster / Campus | Institutional Hierarchy | Group | cluster_id, campus_name | Many universities store campuses as hierarchy nodes |

### xAPI Mapping (Institutional Metadata)

You will use:

- `object.type = "Group" or "Activity"`
- `context.contextActivities.grouping = University / College / Department`
- `context.extensions = { hierarchy values }`

---

## 1.2 Courses, Sections & Descriptions

| Blackboard Entity | API Source | xAPI Type | Extractable Fields |
|------------------|------------|-----------|---------------------|
| Course | Courses API | Activity | courseId, courseName, courseCode, description, created, modified |
| Course Description | Courses API | Activity Definition | description, objectives |
| Course Section (Ultra term section) | Course Membership API | Activity | sectionId, sectionNumber, term, instructors |
| Enrollment | Enrollment API | Statement context | enrollment role, start/end dates |
| Instructor | Users API | Agent | id, name, email, role |
| Teaching Assistants | Users API | Agent | id, name, role |

### xAPI Mapping (Course Metadata)

- `object.type = "Activity"`
- `object.definition.type = "http://adlnet.gov/expapi/activities/course"`
- `context.grouping = university → college → department → program → term → course`

---

## 1.3 Learning Content & Educational Materials

| Blackboard Entity | API Source | xAPI Object Type | Includes |
|-------------------|------------|------------------|----------|
| Ultra Document | Content API | Activity | name, id, parent folder, description |
| Folder / Learning Module | Content API | Activity | structure, hierarchy |
| Assignment | Assignments API | Activity | instructions, attachments |
| Test / Quiz | Assessment API | Activity | questions, metadata |
| File / PDF / Media | Content API | Activity | filename, type |
| External Tool (LTI) | LTI tool data | Activity | launch URL |

---

## 1.4 Academic Engagement Events

| Blackboard Event | Extract Source | xAPI Verb | xAPI Object |
|------------------|----------------|-----------|--------------|
| Course accessed | Activity log | accessed | Course activity |
| Content viewed | Activity log | viewed | Document/file/assessment |
| Assignment submitted | Grades/Attempts API | submitted | Assignment |
| Attempt completed | Assessment API | completed | Quiz/test |
| Question answered | Assessment API | answered | Question |
| Grade posted | Gradebook API | graded | Assignment/Assessment |
| Discussion post | Discussion API | posted | Thread/post |
| Collaborate session join | Collaborate session logs | attended | Session |
| Collaborate chat message | Collaborate logs | commented | Message |

---

# 2. Sample xAPI Statements

Covering all academic-structure metadata and learning events with university tracking.

---

## 2.1 Sample: Course Accessed

Tracks: university → college → department → program → course → section → term.

```json
{
  "actor": {
    "objectType": "Agent",
    "account": {
      "homePage": "https://bb.example.com",
      "name": "student_98321"
    }
  },
  "verb": {
    "id": "http://adlnet.gov/expapi/verbs/accessed",
    "display": {"en-US": "accessed"}
  },
  "object": {
    "id": "https://bb.example.com/courses/ENG101-F23-001",
    "definition": {
      "type": "http://adlnet.gov/expapi/activities/course",
      "name": {"en-US": "English Composition I"},
      "description": {"en-US": "An introductory writing course."}
    }
  },
  "context": {
    "contextActivities": {
      "grouping": [
        { "id": "https://bb.example.com/institution/UniversityA" },
        { "id": "https://bb.example.com/college/ArtsHumanities" },
        { "id": "https://bb.example.com/department/English" },
        { "id": "https://bb.example.com/program/BachelorEnglish" },
        { "id": "https://bb.example.com/term/2023-Fall" },
        { "id": "https://bb.example.com/course/ENG101" }
      ],
      "parent": [
        { "id": "https://bb.example.com/section/ENG101-F23-001" }
      ]
    }
  },
  "timestamp": "2024-02-15T09:32:12Z"
}
