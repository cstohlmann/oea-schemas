# Student Portrait Schema Solution

## Analytikus-Defined Schema

|# | Input | Description | Update Frequency |
|-----------|-----------|-----------|-----------|
| 1 | Schools | Faculties Catalog | Start of semester |
| 2 | Programs | Programs catalog | Start of semester |
| 3 | Courses | Course catalog | Start of semester |
| 4 | Term | Catalog of school terms | Start of semester |
| 5 | Classes | Catalog of classes, groups or sections with open registrations for a course and a school term | Start of semester |
| 6 | Users | Catalog of users: students, teachers, coordinators, etc | Start of semester |
| 7 | Student_Enrollments | List of students enrolled by class, group or section | Start of semester |
| 8 | Professor_Enrollments | List of teachers by class, group or section in which they participate | Start of semester |
| 9 | Assignments | List of mandatory assignments | Start of semester |
| 10 | Discussions | List of mandatory forum discussions | Start of semester |
| 11 | Quizzes | List of mandatory quizzes | Start of semester |
| 12 | Lessons | List of lessons or content "objects" that are required | Start of semester |
| 13 | Assignment_Files | List of assignment files submitted by the student | Weekly |
| 14 | Assignment_Attempts | Student attempts to submit an assignment | Weekly |
| 15 | Posts | Student posts in discussion forums | Weekly |
| 16 | Quiz_Attempts | Student Attempts to complete a quiz | Weekly |
| 17 | Lesson_Attempts | Student attempts to complete a lesson or content object | Weekly |
| 18 | Messages | Messages sent by the student | Weekly |
| 19 | Class_Messages | Messages sent by the student associated with a class, group, or section | Weekly |
| 20 | Page_Views | Access to LMS pages | Weekly |
| 21 | Attendance | Student attendance | Weekly |
| 22 | Screener_answers | Answers to the quizzes that Portrait will suggest for certain students | Weekly |
| 23 | Programs_users | Relationship between students and programs in which they are enrolled | Weekly |
| 24 | Courses_programs | Relationship between courses and programs in which they are taught | Weekly |

## Schema-Related Tables from Moodle


| Table Name | Description | Relevant Table in SPS |
| --- | --- | --- |
| [assign](https://www.examulator.com/er/4.0/tables/assign.html) and/or [assignment_submissions](https://www.examulator.com/er/4.0/tables/assignment_submissions.html) | info around assignments (or assignment submissions). Table is generated from instance of mod_assign  with info. | 9, 13, 14 |
| [Logging 2 API](https://docs.moodle.org/dev/Logging_2) | describes how logs are stored and retrieved. | |
| [Data Manipulation API](https://docs.moodle.org/dev/Data_manipulation_API)| describes how to use available functions to access data from Moodle db - will be important for productionalizing. |  |

## Related-Moodle Schemas
### Assign
<details><summary>Expand Assign Schema</summary>
<p>

Moodle - Assign Table:
| Column Name | Column Type | Description |
| --- | --- | --- |
| id | int | general assignment id |
| course | int | |
| name |  |  |

</p>
</details>

Possible relevant Moodle APIs:
| API | Description | Relevant to Table in SPS |
| --- | --- | --- |
| [Events API](https://docs.moodle.org/dev/Events_API) | allows you to log events in Moddle (Think this is to be used with Logging API). | |
| [Logging 2 API](https://docs.moodle.org/dev/Logging_2) | describes how logs are stored and retrieved. | |
| [Data Manipulation API](https://docs.moodle.org/dev/Data_manipulation_API)| describes how to use available functions to access data from Moodle db - will be important for productionalizing. | [x] |

Other relevant resources
| Resource | Description |
| --- | --- |
| [Data formats documentation](https://www.examulator.com/er/4.0/tables/assign.html) | This table saves information about an instance of ```mod_assign```; whenever an assignment is modified |
| [Teacher-Level Progress Tracking](https://docs.moodle.org/400/en/Tracking_progress) | explains how Moodle can be used by teachers to track course progress - also can be |
| [Moodle Database Schema info](https://moodledev.io/docs/apis/core/dml/database-schema) | Moodle db Schema definitions of Tables. |

