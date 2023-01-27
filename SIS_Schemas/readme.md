> **Note:** This module is not currently released.

<img align="right" height="75" src="https://github.com/microsoft/OpenEduAnalytics/blob/main/docs/pics/oea-logo-nobg.png">

# SIS Schemas

School Information System (SIS) data includes any source that collects relevant data pertaining to schools, classes, students, instructors, class-enrollment, or semester details. While data sources and formats can widely vary, SIS data is often statically formatted (i.e. infrequently changes) including user IDs, school/class/student/instructor names, and further details of schools/classes/students/instructor in an education system. The OEA SIS Schema standards adopt the [Caliper Analytics Specification](https://www.imsglobal.org/spec/caliper/v1p2) in a simplified way suitable for typical education use-cases.

## Caliper Analytics Specification: Agent Entity

[IMS Caliper Analytics](https://www.imsglobal.org/spec/caliper/v1p2) is a technical specification that describes a structured set of vocabulary that assists institutions in collecting SIS data from digital resources, applications, and learning tools. This data can be used to present information to students, instructors, advisers, and administrators to drive effective decision making and promote learner success.

The SIS Schemas adapts the related, following Caliper standards to any SIS data (see the relevant data sources/OEA modules that have been integrated, below) within an education environment:
 - [*Agent Entity*](https://www.imsglobal.org/spec/caliper/v1p2#agent) - general Caliper standard for an abstracted agent.
     * [**Person-Agent Entity**](https://www.imsglobal.org/spec/caliper/v1p2#Person) - used as guidance to build the OEA-standard Student and Instructor schemas.
     * [**Organization-Agent Entity**](https://www.imsglobal.org/spec/caliper/v1p2#Organization) - used as guidance to build the OEA-standard Class, Course, and School schema.
 - [**](https://www.imsglobal.org/spec/caliper/v1p2#Person)
 - [Membership Entity](https://www.imsglobal.org/spec/caliper/v1p2#membership) - used to build the OEA standard Enrollment table.
 - 

## SIS Schema Structures

The OEA SIS Schemas consist of a x tables, which any SIS data can be mapped to. The resulting table is stored in Stage 2.

### Student Table Schema

Two Student tables are created upon standardization: one for general (hashed/masked fields) and one for sensitive (unhashed/unmasked fields). Caliper uses nested JSON arrays, whereas this table is flattened and modified for relevance, with the following specifications.

**[This table is very different from the Caliper standard (since their table contents are abstracted). Double-check if this is to be the OEA-adopted standard.]**

| Column | Description |
| --- | --- |
| student_id | **[student_id or person_id?]** Unique identifier of the student. (hashed in stage2, general) |
| student_grade | Grade-level of the student. |
| student_graduation | Expected date, month-year, or year of graduation for the student. |
| student_birthDate | Student date of birth. (masked in stage2, general) |
| student_birthCity | Student city of birth. (masked in stage2, general) |
| student_birthState | Student state of birth. (masked in stage2, general) |
| student_address | Current recorded address of the student. (masked in stage2, general) |
| student_demographic_race | Racial demographic of the student. |
| student_demographic_ethnicity | Ethnicity demographic of the student. |
| student_demographic_economicStatus | Economic status demographic of the student. |
| student_demographic_esl | English-as-a-Second-Language flag of the student. |
| student_demographic_gender | Gender of the student. |
| student_demographic_adjustedLearning | Flag of whether the student has adjusted learning, and the type of adjusted learning (e.g. 504-Plan). |
| person_type | Student, teacher/professor, or staff identifier; here, all rows are defaulted to "Student". |
| person_surname | Surname, or last name, of the person. (masked in stage2, general) |
| person_givenName | Given name, or first name, of the person. (masked in stage2, general) |
| person_middleName | Middle name of the person. (masked in stage2, general) |
| person_active | Flag of whether the person is currently enrolled/active in the education system. |
| entity_object | Name of the original data source, such as M365. |
| entity_upn | User Principal Name given from the original data source, which acts as a secondary identifier. (hashed in stage2, general) |
| profile_dateCreated | Date/timestamp the student profile was added to the education system. |
| profile_dateModified | Date/timestamp the student was last modified in the education system. |

### Instructor Table Schema

Two Instructor tables are created upon standardization: one for general (hashed/masked fields) and one for sensitive (unhashed/unmasked fields). Caliper uses nested JSON arrays, whereas this table is flattened and modified for relevance, with the following specifications.

**[This table is very different from the Caliper standard (since their table contents are abstracted). Double-check if this is to be the OEA-adopted standard.]**

| Column | Description |
| --- | --- |
| instructor_id | **[instructor_id or person_id?]** Unique identifier of the instructor. (hashed in stage2, general) |
| person_type | Student, teacher/professor, or staff identifier; here, all rows are either "Teacher" or "Professor". |
| person_surname | Surname, or last name, of the person. (masked in stage2, general) |
| person_givenName | Given name, or first name, of the person. (masked in stage2, general) |
| person_middleName | Middle name of the person. (masked in stage2, general) |
| person_active | Flag of whether the person is currently enrolled/active in the education system. |
| entity_object | Name of the original data source, such as M365. |
| entity_upn | User Principal Name given from the original data source, which acts as a secondary identifier. (hashed in stage2, general) |
| profile_dateCreated | Date/timestamp the instructor profile was added to the education system. |
| profile_dateModified | Date/timestamp the instructor profile was last modified in the education system. |

### Class Table Schema

Caliper uses nested JSON arrays, whereas this table is flattened and modified for relevance, with the following specifications.

**[This table is very different from the Caliper standard (since their table contents are abstracted). Double-check if this is to be the OEA-adopted standard.]**

| Column | Description |
| --- | --- |
| class_id | **[class_id, section_id, or organization_id?]** Unique identifier of the class. |
| class_name | Name of the class. |
| class_section | Section identifier of the class. |
| class_instructor | Number of students enrolled in the class. |
| class_startDate | Start date of the class. |
| class_endDate | End date of the class. |
| class_calendarCycle | The calendar cycle that the class is a part of (e.g. Spring2022). |
| class_enroll | The number of students enrolled in the class. |
| class_meetingType | Main teaching-format of the class (e.g. In-Person, Hybrid, Online/Remote). |
| class_meetingNums | Number of regular meetings of the class (e.g. 2, 3, 5). |
| class_meetingDays | Days-of-the-week the class regularly meets (e.g. MWF, Monday Wednesday Friday). |
| class_meetingTime | Time-of-day the class is scheduled to meet (e.g. 12:15, 1 PM). |
| class_active | Flag of whether the class is currently active. |
| class_subOrganizationOf | The over-arching course ID to which the class belongs. |
| entity_object | Name of the original data source, such as M365. |
| profile_dateCreated | Date/timestamp the class profile was added to the education system. |
| profile_dateModified | Date/timestamp the class profile was last modified in the education system. |

### Course Table Schema

Caliper uses nested JSON arrays, whereas this table is flattened and modified for relevance, with the following specifications.

**[This table is very different from the Caliper standard (since their table contents are abstracted). Double-check if this is to be the OEA-adopted standard.]**

| Column | Description |
| --- | --- |
| course_id | **[course_id, organization_id or other?]** Unique identifier of the course. |
| course_name | Name of the course in the education system. |
| course_type | Type of course, such as art, history, science, math, etc. |
| course_numClasses | The total number of classes/sections being currently taught in the education system. |
| course_enroll | Number of students enrolled in the course (i.e. aggregate number of students in each class/section). |
| course_gradeLevel | Grade-level of the course (e.g. 1st year, undergraduate, second grade). |
| course_active | Flag of whether the course is currently active. |
| course_subOrganizationOf | The over-arching school ID to which the course belongs. |
| entity_object | Name of the original data source, such as M365. |
| profile_dateCreated | Date/timestamp the course profile was added to the education system. |
| profile_dateModified | Date/timestamp the course profile was last modified in the education system. |

### School Table Schema

Two School tables are created upon standardization: one for general (hashed/masked fields) and one for sensitive (unhashed/unmasked fields). Caliper uses nested JSON arrays, whereas this table is flattened and modified for relevance, with the following specifications.

**[This table is very different from the Caliper standard (since their table contents are abstracted). Double-check if this is to be the OEA-adopted standard.]**

| Column | Description |
| --- | --- |
| school_id | **[school_id or organization_id?]** Unique identifier of the school. |
| school_name | Name of the school in the education system. |
| school_type | Type of school in the education system, such as Pre-K, Elementary, Middle, High, College, etc. |
| school_address | Address of thae school. |
| school_country | Country of the school's location. |
| school_latitude | Latitude of the school's location. (masked in stage2, general) |
| school_longitude | Longitude of the school's location. (masked in stage2, general) |
| school_coursesOffered | Number of courses currently offered by the school. |
| school_subOrganizationOf | The name of the overarching education system, to which the school belongs. |
| entity_object | Name of the original data source, such as M365. |
| profile_dateCreated | Date/timestamp the school profile was added to the education system. |
| profile_dateModified | Date/timestamp the school profile was last modified in the education system. |

## Schema Setup Instructions

<p align="center">
  <img src="https://github.com/microsoft/OpenEduAnalytics/blob/main/schemas/schema_catalog/Digital_Engagement_Schema/docs/images/digital_engagement_schema_setup.png" alt="OEA Digital Engagement Standard Schema Setup Instructions"/>
</p>

<ins><strong>Preparation:</ins></strong> Ensure you have proper [Azure subscription and credentials](https://github.com/microsoft/OpenEduAnalytics/tree/main/framework) and setup the [most recent version of OEA framework](https://github.com/microsoft/OpenEduAnalytics/tree/main/framework#setup-of-framework-assets). This will include the most recent version of the [OEA python class](https://github.com/microsoft/OpenEduAnalytics/blob/main/framework/synapse/notebook/OEA_py.ipynb).

To standardize digital engagment data into the OEA Digital Engagement Schema, complete the following steps:

- Examine available digital engagement data in Stage2p. Examples of digital engagement data listed [below](https://github.com/microsoft/OpenEduAnalytics/tree/main/schemas/schema_catalog/Digital_Engagement_Schema#related-oea-modules)
- Import the [Schema_DigitalActivity_py](https://github.com/microsoft/OpenEduAnalytics/blob/main/schemas/schema_catalog/Digital_Engagement_Schema/notebook/Schema_DigitalActivity_py.ipynb) python class to process data in the [DigitalActivity_main_pipeline](https://github.com/microsoft/OpenEduAnalytics/blob/main/schemas/schema_catalog/Digital_Engagement_Schema/pipeline/DigitalActivity_main_pipeline.zip). The main step here is to map the source data schema to the Digital Engagment Schema. Examples of data processing are given in the class notebook. 
- Import the [Digital Activity Schema pipeline template](https://github.com/microsoft/OpenEduAnalytics/blob/main/schemas/schema_catalog/Digital_Engagement_Schema/pipeline/DigitalActivity_main_pipeline.zip) into your Synapse workspace and execute the pipeline; ensure you are standardizing data from the desired modules. See the [schema pipeline page](https://github.com/microsoft/OpenEduAnalytics/tree/main/schemas/schema_catalog/Digital_Engagement_Schema/pipeline) for detailed instructions.
- Verify that standardized Digital Engagement data is stored in Stage2p in the digital_activity folder.
- Set up the schema standardization to be used for the packages/use cases needed.

## Related [OEA Modules](https://github.com/microsoft/OpenEduAnalytics/tree/main/modules/module_catalog)

The OEA Digital Engagement Schema can be applied to the following OEA Modules:

| Module | Applicable Tables |
| --- | --- |
| [Microsoft Education Insights](https://github.com/microsoft/OpenEduAnalytics/tree/main/modules/module_catalog/Microsoft_Education_Insights) Module | The ApplicationUsage/"TechActivity" table. |
| [Microsoft Graph](https://github.com/microsoft/OpenEduAnalytics/tree/main/modules/module_catalog/Microsoft_Graph) Module | The Microsoft 365 Applications User Detail and Teams Activity User Detail tables. |
| [Clever](https://github.com/microsoft/OpenEduAnalytics/tree/main/modules/module_catalog/Clever) Module | The Daily Participation and Resource Usage tables. |
| [i-Ready](https://github.com/microsoft/OpenEduAnalytics/tree/main/modules/module_catalog/iReady) Module | The Comprehensive Student Lesson Activity with Standards (ELA and Math) tables. |

See the demo processing notebook in the [Notebook resource](https://github.com/microsoft/OpenEduAnalytics/tree/main/schemas/schema_catalog/Digital_Engagement_Schema/notebook) for an example of standard schema application.

## Technical Assets

This OEA Digital Engagement Schema provides the following assets:
 - [Notebooks](https://github.com/microsoft/OpenEduAnalytics/tree/main/schemas/schema_catalog/Digital_Engagement_Schema/notebook):
     * one [digital activity schema standard](https://github.com/microsoft/OpenEduAnalytics/blob/main/schemas/schema_catalog/Digital_Engagement_Schema/notebook/Schema_DigitalActivity_py.ipynb) class notebook (contains the necessary functions for standardizing a data source with digital activity), and 
     * one [demo processing notebook](https://github.com/microsoft/OpenEduAnalytics/blob/main/schemas/schema_catalog/Digital_Engagement_Schema/notebook/Schema_DigitalActivity_Demo.ipynb) (used for demonstration of the schema-standardization utility and functionality).
 - [Pipeline](https://github.com/microsoft/OpenEduAnalytics/tree/main/schemas/schema_catalog/Digital_Engagement_Schema/pipeline): Sample main pipeline used to process digital engagement data into this schema.

## Contributions from the Community
 
The OEA SIS Schema Standard [welcomes contributions](https://github.com/microsoft/OpenEduAnalytics/blob/main/docs/license/CONTRIBUTING.md).

This standard was developed by [Kwantum Analytics](https://www.kwantumedu.com/) using IMS Global's Caliper standard as guidance. The architecture and reference implementation for all modules is built on [Azure Synapse Analytics](https://azure.microsoft.com/en-us/services/synapse-analytics/) - with [Azure Data Lake Storage](https://docs.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction) as the storage backbone,  and [Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/) providing the role-based access control.

# Legal Notices
Microsoft and any contributors grant you a license to the Microsoft documentation and other content
in this repository under the [Creative Commons Attribution 4.0 International Public License](https://creativecommons.org/licenses/by/4.0/legalcode),
see the [LICENSE](LICENSE) file, and grant you a license to any code in the repository under the [MIT License](https://opensource.org/licenses/MIT), see the
[LICENSE-CODE](LICENSE-CODE) file.

Microsoft, Windows, Microsoft Azure and/or other Microsoft products and services referenced in the documentation
may be either trademarks or registered trademarks of Microsoft in the United States and/or other countries.
The licenses for this project do not grant you rights to use any Microsoft names, logos, or trademarks.
Microsoft's general trademark guidelines can be found at http://go.microsoft.com/fwlink/?LinkID=254653.

Privacy information can be found at https://privacy.microsoft.com/en-us/

Microsoft and any contributors reserve all other rights, whether under their respective copyrights, patents,
or trademarks, whether by implication, estoppel or otherwise.

