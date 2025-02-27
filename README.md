# Student Grade Tracker

A comprehensive student grade tracker that uses CSV files, organized folder structures (including a **"Reports"** folder for data visualizations), and integrates various data structures—**lists**, **dictionaries**, **tuples**, and **sets**—to simulate realistic data analysis and reporting. The project generates fake data for students, courses, and grades (with grades following a normal distribution), then saves and plots the data using popular Python libraries.

## Table of Contents

- [Features](#features)
- [Installation & Setup](#installation--setup)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [Data Generation Details](#data-generation-details)
- [Data Structures & Functionalities](#data-structures--functionalities)
- [Links](#links)
- [License](#license)

## Features

- **CSV Filing System & Directory Structure:**
  - Creates a main folder named **"Student Grade Tracker"**
  - Generates separate CSV files for:
    - **Students**
    - **Courses**
    - **Grades**
  - Creates a **"Reports"** subfolder that stores saved plots and visualizations
- **Data Generation:**
  - Uses the [Faker](https://faker.readthedocs.io/) library for realistic student names and emails
  - **Grade Generation Approaches:**
    - **Initial Approach (Uniform Distribution):**  
      Initially, grades were generated using a random number generator:
      ```python
      for student in students_list:
          for course in courses_list:
              grade = random.randint(50, 100)
              gm.add_grade(student.student_id, course.course_id, grade, "Fall 2024")
      ```
      This produced a uniform distribution that looked unrealistic.
    - **Improved Approach (Normal Distribution):**  
      Grades are now generated using a normal distribution to create a realistic bell curve, and students are randomly assigned to a subset of courses:
      ```python
      # For each student, assign a random grade for a randomly selected subset of courses
      for student in students_list:
          num_courses_for_student = random.randint(2, 4)
          selected_courses = random.sample(courses_list, num_courses_for_student)
          
          for course in selected_courses:
              mean_grade = 75
              std_dev = 10
              generated_grade = np.random.normal(loc=mean_grade, scale=std_dev)
              generated_grade = int(round(generated_grade))
              generated_grade = max(0, min(100, generated_grade))
              gm.add_grade(student.student_id, course.course_id, generated_grade, "Fall 2024")
      ```
- **Data Analysis & Visualization:**
  - Visualizations are created using [Matplotlib](https://matplotlib.org/) and [Seaborn](https://seaborn.pydata.org/)
- **Integration of Data Structures:**
  - **Lists & Dictionaries:**  
    Used to store collections of student and course objects
  - **Tuples:**  
    The `get_student_tuple` function in `GradeManager` returns a tuple containing a student's ID, name, and email
  - **Sets:**  
    The `get_students_in_course` function returns a set of student IDs for a given course, enabling set intersections to find students enrolled in multiple courses

## Installation & Setup

### Prerequisites

- Python 3.6 or higher
- [pip](https://pip.pypa.io/en/stable/)

### Installing Dependencies

You can install the required libraries either individually or via a `requirements.txt` file:

**Individual Installation:**

```bash
pip install pandas numpy matplotlib seaborn faker
```

Or, if you have a requirements.txt:

```bash
pip install -r requirements.txt
```

### Google Drive Setup (Optional)

If you're running this in Google Colab:

1. Mount Google Drive in your notebook:

```python
from google.colab import drive
drive.mount('/content/drive')
```

2. Directory Structure:
   - The project will create the required directory structure in your Google Drive under "My Drive/Student Grade Tracker"

## Usage

### Clone or Download the Repository

```bash
git clone https://github.com/yourusername/student-grade-tracker.git
cd student-grade-tracker
```

### Run the Project

1. Open the main project file in your preferred IDE or Jupyter Notebook
2. Execute the cells in order to:
   - Generate fake data
   - Save CSV files to the designated directory
   - Generate and save plots in the "Reports" folder
3. If running in Google Colab, ensure Google Drive is mounted correctly

### Viewing Data & Reports

- **CSV Files:**
  - Check the CSV files in your "Student Grade Tracker" folder on Google Drive
- **Reports:**
  - Open the "Reports" folder to view saved visualizations

## Project Structure

```
student-grade-tracker/
├── README.md
├── requirements.txt
└── main_notebook.ipynb  (or main.py)
```

- **CSV Files:**
  - Stored under `/content/drive/My Drive/Student Grade Tracker/` (or a similar folder on your local machine if modified)
- **Reports:**
  - Saved under `/content/drive/My Drive/Student Grade Tracker/reports/`

## Data Generation Details

### Grade Generation Approaches

#### Initial Approach (Uniform Distribution)

Grades were initially generated using a uniform random integer between 50 and 100:

```python
for student in students_list:
    for course in courses_list:
        grade = random.randint(50, 100)
        gm.add_grade(student.student_id, course.course_id, grade, "Fall 2024")
```

This approach produced a uniform distribution that did not mimic real-world grading patterns.

#### Improved Approach (Normal Distribution)

To create a more realistic bell-curve distribution, the code was updated to generate grades using a normal distribution. Also, students are randomly assigned to a subset of courses:

```python
# For each student, assign a random grade for a randomly selected subset of courses
for student in students_list:
    num_courses_for_student = random.randint(2, 4)
    selected_courses = random.sample(courses_list, num_courses_for_student)
    
    for course in selected_courses:
        mean_grade = 75
        std_dev = 10
        generated_grade = np.random.normal(loc=mean_grade, scale=std_dev)
        generated_grade = int(round(generated_grade))
        generated_grade = max(0, min(100, generated_grade))
        gm.add_grade(student.student_id, course.course_id, generated_grade, "Fall 2024")
```

This approach not only creates a realistic distribution of grades but also simulates selective enrollment across courses—enabling the use of set intersections to analyze common enrollments.

## Image Demonstration
<p align="center">
  <img src="Grade Distribution Plots/course_102_distribution.png" alt="Grade Distribution for Course 102" width="600">
  <br>
  <em>Grade distribution for History, demonstrating statistical modelling applied to simulate real-world student performance trends.</em>
</p>

<p align="center">
  <img src="Grade Distribution Plots/course_103_distribution (1).png" alt="Grade Distribution for Course 103" width="600">
  <br>
  <em>Grade distribution for Biology.</em>
</p>

<p align="center">
  <img src="Grade Distribution Plots/Grades CSV Database.png" alt="Student Grades CSV" width="600">
  <br>
  <em>Sample of the grades.csv file containing student IDs, course information, grades, and semester data for Fall 2024.</em>
</p>

<p align="center">
  <img src="Grade Distribution Plots/Visualisations Folder.png" alt="Visualisation Folder" width="600">
  <br>
  <em>Visualisation folder in Google Drive containing generated plots for various courses, including the grade distributions for History (102) and Biology (103).</em>
</p>

<p align="center">
  <img src="Grade Distribution Plots/Main directory.png" alt="Project Directory" width="600">
  <br>
  <em>Main project directory structure showing the data files (courses.csv, grades.csv, students.csv) and reports folder for the Student Grade Tracker system.</em>
</p>

## Data Structures & Functionalities

### Lists & Dictionaries

Used to store collections of student and course objects.

### Tuples

The `get_student_tuple` function in GradeManager returns a tuple containing:

```python
def get_student_tuple(self, student_id: int) -> tuple:
    student_row = self.students[self.students["student_id"] == student_id]
    if student_row.empty:
        return None
    row = student_row.iloc[0]
    return (row["student_id"], row["name"], row["email"])
```

### Sets

The `get_students_in_course` function returns a set of student IDs for a given course:

```python
def get_students_in_course(self, course_id: int) -> set:
    return set(self.grades[self.grades["course_id"] == course_id]["student_id"])
```

This functionality allows using set intersections to determine which students are enrolled in multiple courses.

## Links

### Google Colab Notebook
[Open the Student Grade Tracker Notebook](https://colab.research.google.com/drive/1jElH4KJVXBnoy3eM5ftUidk3VSANCJ3E#scrollTo=LLeay4jsaCuh)


### GitHub Repository
[GitHub - mjassiri/student-grade-tracker](https://github.com/mjassiri/Student-Grade-Tracker)

## License

This project is licensed under the MIT License.
