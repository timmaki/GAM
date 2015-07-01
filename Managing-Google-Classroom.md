- [Managing Courses](#managing-courses)
  - [Creating A Course](#creating-a-course)
  - [Updating A Course](#updating-a-course)
  - [Getting Course Info](#getting-course-info)
  - [Deleting A Course](#deleting-a-course)
- [Managing Course Participants](#managing-course-participants)
  - [Adding Students And Teachers To A Course](#adding-students-and-teachers-to-a-course)
  - [Syncing Students And Teachers To A Course](#syncing-students-and-teachers-to-a-course)
  - [Removing Students And Teachers From A Course](#removing-students-and-teachers-from-a-course)
- [Course And Course Participant Reports](#course-and-course-participant-reports)
  - [Printing Courses](#printing-courses)
  - [Printing Course Participants](#printing-course-participants)

# Managing Courses
## Creating A Course
### Syntax
```
gam create course [alias <alias>] [name <name>] [section <section>] [heading <heading>] [description <description>] [room <room>] [teacher <teacher email>] [status <PROVISIONED|ACTIVE|ARCHIVED|DECLINED>]
```
Provision a new course. The optional alias parameter provides a unique id which can be used to reference the course. If a course already exists with this alias, an error will be thrown. If no alias is supplied, the course must be managed by the id that is assigned to it by Google when created. The optional name, section, heading, description and room parameters provide additional details for the course. The optional teacher parameter provides the email address of the owner / primary teacher of the course. If no teacher is provided then the admin user running GAM will be the owner / primary teacher of the course. The optional status parameter provides the initial status of the course when created. If no status is provided, courses default to PROVISIONED status.

### Example
This example creates a course.
```
gam create course alias the-republic-s01 name "The Republic" section s01 heading "The definition of justice (δικαιοσύνη), the order and character of the just city-state and the just man" room academy-01 teacher plato@athens.edu
```
----

## Updating A Course
### Syntax
```
gam update course <id or alias> [name <name>] [section <section>] [heading <heading>] [description <description>] [room <room>] [status <PROVISIONED|ACTIVE|ARCHIVED|DECLINED>]
```
Updates an existing course. The id or alias of the course is needed to identify the exact course to be updated. The optional name, section, heading, description and room parameters provide additional details for the course. The optional status parameter sets the status of the course.

### Example
This example updates an existing course to make it active
```
gam update course the-republic-s01 status ACTIVE
```
----
## Getting Course Info
### Syntax
```
gam info course <id or alias>
```
Prints detailed information about a course.

### Example
This example prints information about the course
```
gam info course the-republic-s01
updateTime: 2015-07-01T13:47:20.000Z
room: academy-01
alternateLink: http://classroom.google.com/c/MtM0NzcxNDY5
enrollmentCode: 46rvtp
section: s01
creationTime: 2015-07-01T13:47:20.000Z
courseState: ACTIVE
ownerId: 102043113942954782808
id: 134781269
descriptionHeading: The definition of justice (δικαιοσύνη), the order and character of the just city-state and the just man
name: The Republic
Aliases:
  the-republic-s01
Participants:
 Teachers:
  Plato Plato - plato@athens.edu
 Students:
```
----

## Deleting A Course
### Syntax
```
gam delete course <id or alias>
```
Deletes the given course.

### Example
This example deletes the course
```
gam delete course the-republic-s01
```
----

# Managing Course Participants
## Adding Students And Teachers To A Course
### Syntax
```
gam course <id or alias> add student|teacher <email address>
```
Add the given user email address to the course as a student or teacher.

### Example
This example adds Aristotle as a student in the course
```
gam course the-republic-s01 add student aristotle@athens.edu
```
----

## Syncing Students And Teachers To A Course
### Syntax
```
gam course <id or alias> sync students|teachers group <group email> | ou <orgunit> | file <filename> | query <users query> | course <id or alias>
```
Syncs the students or teachers for the given course against another list of users. Students/Teachers not in the other list will be removed from the given course. Students/Teachers in the other list but not the course will be added.

### Examples
This example adds all users in the Google Org Unit /schools/sunnybrook/K-1 into the course. If there are students in the course that are not in this OU, they will be removed.
```
gam course sunnybrook-k-1 sync students ou /schools/sunnybrook/K-1
```
This example syncs the course teachers against members of the biology-101-teachers@sunnybrook.edu group.
```
gam course biology-101-s01 sync teachers group biology-101-teachers@sunnybrook.edu
```
This example syncs course students against a CSV file
```
gam course history-200-s02 sync students file history-200-s02-students.csv
```
----

## Removing Students And Teachers From A Course
### Syntax
```
gam course <id or alias> remove student|teacher <email address>
```
removes the given email address from the course as a student or teacher.

### Example
This example removes John from the course.
```
gam update course the-republic-s01 remove student john@athens.edu
```
----

# Course And Course Participant Reports
## Printing Courses
### Syntax
```
gam print courses [teacher <email>] [student <email>] [todrive]
```
Output CSV format details of courses. By default, all courses in the organization will be returned. The optional teacher and student parameters limit the results to courses where the given user is a participant in the course of the given type. The optional todrive argument creates a Google Drive spreadsheet of the results rather than outputting the information to the console.

### Examples
This example creates a CSV file of all courses
```
gam print courses
```
this example creates a Google Spreadsheet of all the courses Mr. Smith is teaching
```
gam print courses teacher mrsmith@acme.edu todrive
```
----

## Printing Course Participants
### Syntax
```
gam print course-participants [course <id or alias>] [student <email>] [teacher <email>] [todrive]
```
Output CSV format details of course participants. The optional course parameter limits results to the given course. Multiple course parameters can be included to pull participants for a subset of courses. If no course parameter is specified then participants will be retrieved for all courses. The optional student and teacher parameters limit the courses returned to those where the given user is a teacher or student. The optional todrive argument creates a Google Drive spreadsheet of the results rather than outputting the information to the console.

### Examples
This example prints all course participants in all courses.
```
gam print course-participants
```
this example creates a spreadsheet of the course participants in all three sections of Chemistry.
```
gam print course-participants course chemistry-101-s01 course chemistry-101-s02 course chemestry-101-s03 todrive
```
----