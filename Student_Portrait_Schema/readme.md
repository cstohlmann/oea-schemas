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

Table details pulled from: [Moodle 4.0 Database Schema info](https://www.examulator.com/er/4.0/)

| Table Name | Description | Relevant Table in SPS |
| --- | --- | --- |
| [course_categories](https://www.examulator.com/er/4.0/tables/course_categories.html) | data around the categories to which each course belongs. (Thinking this acts as a Programs table per schema above?) Thinking this table combined with course, enrollment, users, and roles can be used to develop tables 23 and 24. | 2, 23*, 24* |
| [course](https://www.examulator.com/er/4.0/tables/course.html) | data around courses offered by the system. | 3 |
| [sessions](https://www.examulator.com/er/4.0/tables/sessions.html) | data around sessions in the education system (e.g. Spring 2023). | 4 |
| [course_sections](https://www.examulator.com/er/4.0/tables/course_sections.html) | data around sections/classes per course offered by the system. | 5 |
| [user](https://www.examulator.com/er/4.0/tables/user.html), [role_assignments](https://www.examulator.com/er/4.0/tables/role_assignments.html), and [role](https://www.examulator.com/er/4.0/tables/role.html) | data around users - one record per person in the system (other two tables are necessary to distinguish students from instructors). | 6 |
| [enrol](https://www.examulator.com/er/4.0/tables/enrol.html) and [user_enrolments](https://www.examulator.com/er/4.0/tables/user_enrolments.html) | data around users enrollment, maps enrol and user tables together to separate student vs. instructor enrollment. | 7, 8 |
| [assign](https://www.examulator.com/er/4.0/tables/assign.html) [assign_user_mapping](https://www.examulator.com/er/4.0/tables/assign_user_mapping.html), [assignment](https://www.examulator.com/er/4.0/tables/assignment.html) and/or [assignment_submissions](https://www.examulator.com/er/4.0/tables/assignment_submissions.html) | describes info around assignments (or assignment submissions). Table is generated from instance of mod_assign with info. assign_user_mapping is needed to map assignments relevant to particular users. | 9, 14 |
| [forum](https://www.examulator.com/er/4.0/tables/forum.html) | data around forums and structured/assigned discussions. | 10 |
| [quiz](https://www.examulator.com/er/4.0/tables/quiz.html), [quiz_attempts](https://www.examulator.com/er/4.0/tables/quiz_attempts.html), and [quiz_grades](https://www.examulator.com/er/4.0/tables/quiz_grades.html) | data around quizzes and student-quiz attempts. | 11, 16 |
| [lesson](https://www.examulator.com/er/4.0/tables/lesson.html) and [lesson_attempts](https://www.examulator.com/er/4.0/tables/lesson_attempts.html) (maybe [lesson_answers](https://www.examulator.com/er/4.0/tables/lesson_answers.html) as well) | data around lessons and student-lesson attempts. | 12, 17 |
| [assignsubmission_file](https://www.examulator.com/er/4.0/tables/assignsubmission_file.html) | describes info around assignment file submissions. | 13 |
| [post](https://www.examulator.com/er/4.0/tables/post.html) and/or [forum_posts](https://www.examulator.com/er/4.0/tables/forum_posts.html) | data around posts/blog-entries recorded. Second table contains data surrounding forum-specific posts. | 15, 10* |
| [messages](https://www.examulator.com/er/4.0/tables/assign.html) and/or [message_user_actions](https://www.examulator.com/er/4.0/tables/message_user_actions.html) | data around messages throughout the system (or, in the second case, message actions per-user). | 18, 19*, 10* |


*NOTE: * indicates uncertainty if this is completely applicable.*

Additional (possibly useful tables):
| Table Name | Description |
| --- | --- |
| [stats_daily](https://www.examulator.com/er/4.0/tables/stats_daily.html) | Moodle generated daily stats per course/role (think this breaks down stats at a per-user-level). |
| [user_lastaccess](https://www.examulator.com/er/4.0/tables/user_lastaccess.html) | Keeps track of course page access times. Probably most useful for table 20 in the schema. |

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

