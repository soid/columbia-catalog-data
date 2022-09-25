# Columbia University Directory of Classes Data Set

This repository is a data set of all publicly available classes and instructors teaching at Columbia University of the City of New York.
All data is available in JSON and CSV formats. The data set is regularly updated (or supposed to).

All data is crawled from [Columbia Directory](http://www.columbia.edu/cu/bulletin/uwb/) public website.
The crawling scripts are available in the sister repository [soid/columbia-catalog-scraper](https://github.com/soid/columbia-catalog-scraper).  

The data is "enriched" with content from Wikipedia, [CULPA.info](http://culpa.info), and other sources.
Feel free to collaborate on enriching this data set with useful sources (Google Scholar profiles, syllabi links, etc would be cool to add).


## Data description
Most data fields are self explanatory (e.g. "departement" or "wikipedia_link"). 


### List of classes
Files are available in `classes/{YEAR}-{SEMESTER}`. Semester is 'Fall', 'Spring', or 'Summer'.
- `scheduled_time_start` and `scheduled_time_end` are in American time notation: `00:00am/pm`
- strange fields directly correspond to [Columbia Directory](http://www.columbia.edu/cu/bulletin/uwb/) fields, e.g. `call_number` or `class_id`
- `scheduled_days` is a string of any characters "MTWHFSU" each standing for Monday through Sunday accordingly 
- `prerequisites` is a two level list of `course_code` that are course prerequisites. First level joined with an AND, second level is OR. For example, `[['COMS W3134', 'COMS W3137']]` means "(COMS W3134) **or** (COMS W3137)", and `[['COMS W3134'], ['COMS W3137']]` means "(COMS W3134) **and** (COMS W3137)".
- `gta` is the year of Great Teacher Award if applicable

### List of instructors

Instructors for all semesters available as a single file in the `instructors/` directory.


## Use Examples

All data is available in JSON and CSV formats. You can easily browse CSV files in Excel, Apple Numbers or the likes. JSON is more appropriate for use in scripting.


### Python Pandas

Reading classes list:
```python
# load fall 2020 semester
>>> import pandas as pd
>>> df = pd.read_json('classes/2020-Fall.json')
>>> print(df)
      course_code                  course_title                     course_descr           instructor scheduled_time_start scheduled_time_end  call_number           campus         class_id                       department department_code            instructor_culpa_link instructor_culpa_nugget  instructor_culpa_reviews_count instructor_wikipedia_link                             link         location method_of_instruction                          open_to points            prerequisites scheduled_days          type
0     ACLS BC3450          WOMEN AND LEADERSHIP  Prerequisites: Permission of...                 None              10:10am            12:00pm          139  Barnard College  X3450-20203-001  Athena Center for Leadership...            ACLS                             None                    None                             NaN                      None  http://www.columbia.edu//cu/...  To be announced             In-person                [Barnard College]      4                       []             MF       SEMINAR
1     ACLS BC3450          WOMEN AND LEADERSHIP  Prerequisites: Permission of...                 None              10:10am            12:00pm          140  Barnard College  X3450-20203-002  Athena Center for Leadership...            ACLS                             None                    None                             NaN                      None  http://www.columbia.edu//cu/...  To be announced             In-person                [Barnard College]      4                       []             MF       SEMINAR
...

# show most listed departments 
>>> print(df.department.value_counts())
Medicine                                                      3751
International and Public Affairs                               302
Dental and Oral Surgery                                        260
Core (A&S)\t                                                   214
Social Work                                                    199

# show classes in computer science department
>>> print(df[df['department'] == 'Computer Science'])
     course_code                    course_title                     course_descr             instructor scheduled_time_start scheduled_time_end  call_number       campus         class_id        department department_code            instructor_culpa_link instructor_culpa_nugget  instructor_culpa_reviews_count        instructor_wikipedia_link                             link         location method_of_instruction                          open_to points                    prerequisites scheduled_days     type
1597  COMS E6113      Topics in Database Systems                             None              Eugene Wu              11:40am            12:55pm        10884  Morningside  E6113-20203-001  Computer Science            COMS  http://culpa.info/professors...                    None                             1.0                             None  http://www.columbia.edu//cu/...  To be announced             In-person  [Barnard College, Columbia C...      3                               []             TR  LECTURE
1598  COMS E6156  TOPICS IN SOFTWARE ENGINEERING  Topics in Software engineeri...      Donald F Ferguson               2:10pm             4:00pm        11991  Morningside  E6156-20203-001  Computer Science            COMS  http://culpa.info/professors...                  silver                             4.0  https://en.wikipedia.org/wik...  http://www.columbia.edu//cu/...  To be announced             In-person  [Barnard College, Columbia C...      3                               []              F  LECTURE
...
```

Reading instructors list: 
```python
>>> import pandas as pd
>>> df = pd.read_json('instructors/instructors.json')
>>> print(df)
```



## Projects

[peqod.com](https://peqod.com) - unofficial catalog of classes

[CUGraph.info](http://cugraph.info) - all Columbia classes visualized as a graph of prerequisites.


If you use this data set in your project, feel free to create a pull request with the link and a description of your project here. 
