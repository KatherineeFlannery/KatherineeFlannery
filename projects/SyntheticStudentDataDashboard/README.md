**Task**

This project is based on a dashboard I made as a teacher when tasked with analyzing and presenting my student data. The purpose was to identify trends and insights to guide instruction.
To protect data privacy and FERPA compliance, this dashboard is made using fully synthetic data generated using Python’s Faker library and contains no real student data. 

**Data**

This is a recreated student-data dashboard built for demonstration purposes. All data in this demo is synthetic and was generated using Faker (seed provided). No real student or personally identifiable information (PII) was used. 
Each row represents one student record, a total of 110 student records were generated. 

[Synthetic Data Code](https://github.com/KatherineeFlannery/KatherineeFlannery/blob/00daa574c16c73b0be8fb4a6a4bed95fc1a05fd8/projects%20/SyntheticStudentDataDashboard/SyntheticStudentData.ipynb)

**Column Titles**

The dataset contains the following columns: 

StudentID, StudentName, Gender, ClassPeriod, Hispanic, SBAC, iReadyScore, 7.GA.1, 7.RP.2AD, 7.RP.A2A, 7.RP.A2B, 7.RP.A2C, 7GB4, AverageAssessment, Current Grade, IEP, 504.


**​SBAC:** Represents the previous year standardized test score. (Smarter Balanced Assessment Consortium).

**iReadyScore:** Most recent i-Ready assessment result for that student.

**7.GA.1, 7.RP.2AD, 7.RP.A.2A, 7.RP.A.2B, 7.RP.A.2C, 7.GB.4:** Represent Common Core math standards evaluated. Each standard is scored with a rubric for proficiency. 

**AverageAssessment:** Aggregates performance across all evaluated standards for each student.

**CurrentGrade:** A letter grade (A–D) generated from the AverageAssessment score using the Excel IFS() function.

**IEP / 504:** Indicate whether a student has an Individualized Education Program (IEP) or a 504 accommodation plan.

**​Cleaning and Orgainizing the Data**

In my original data project, the data was sourced from different places and needed to be merged and cleaned before continuing. There were extra columns that were not needed and missing data. This project uses synthetic data, so I generated the columns that I needed using the Python script. 


After exporting the generated data into a CSV file, I imported it into Excel. I added a column to find the average of the assessments, a grade letter based on the average assessments column, and added two columns with random students in two class periods marked as having and IEP and some students marked as having and 504.

**Pivot Tables and Dashboard**

Once I had all the data required, I looked for patterns using pivot tables and summary statistics. Finally, I used the pivot tables to create pivot charts for my dashboard. I then added slicers and linked them to the different pivot charts to make the dashboard interactive and look for insights to guide instruction. 

