# HR Analytics using PowerBI

HR Analytics is another term for Workforce/People Analytics and is the collection and application of employee data to make decisions around workforce planning. This involves gathering the right data, transforming it, devising suitable KPIs, and visualizing them.
Some use cases of HR Analytics are,

- Identifying gaps in skills: With 'Quiet Hiring' on the rise, identifying general skill deficits or surpluses can help organizations plan learning and development courses
- Analyzing Employee Attrition and its risk: Understanding leading factors for why employees voluntarily leave and how this could have been avoided. Historic data can also be used for predictive analysis to gauge the chance of a current employee leaving based on exhibited behavior
- Improving Hiring: A typical hiring process consists of posting a job, going through applications, screening candidates, and conducting interviews. Data collected at each step, like questions asked, match % of candidate profiles with the Job Description and can be analyzed to understand if they assess candidates well based on their current performance

In this project, I will be taking up one of the use cases of HR Analytics, which is to understand employee behavior and identify underlying patterns,

- Working preference of employees: On-site or remote?
- Working location vs day preferred
- Nature of sick leaves taken

This is a guided project by [Dhaval Patel](https://www.youtube.com/watch?v=ru1qeDO_qrc&list=PLeo1K3hjS3uuVQccZa7yFwK3ltoGQOWbM). The Dataset used is an Attendance sheet shared by the HR of Atliq.

We are using Power BI to transform this data and address the above topics

## Data Tranformation:
This is how the data looks - There is a sheet that pertains to each month of data. Each sheet has the days of the month as columns
![image](https://user-images.githubusercontent.com/27859890/225420705-ce7ff96d-9736-4d29-a322-1163cae65d3d.png)

After adding this Excel file to Power BI, we make tranformations to our data using the Power Query Editor. Since there are different sheets in the Excel file with each of them having different columns, we need to transform the data such that all the data is in a single sheet with uniform headers. 
This is how the editor looks after loading our file - 

![image](https://user-images.githubusercontent.com/27859890/225422818-9d0ebff0-7fa1-4bfa-98df-7540d49369f0.png)

We will now make transformations on one of the rows of the table (corresponding to one sheet of the file) and then expand it to the remaining sheets. The transformations we make are,
- Converting the first row of data to headers
- Deleting the top most row after that as it serves no purpose
- Renaming columns
- Unpivoting the date columns to have them all in a single column
- Changing the types of the columns 
- Removing errors from the date column

We then create a new parameter that will dynamically identify sheets of our source file and can be used to filter out data based on the sheet name.

![image](https://user-images.githubusercontent.com/27859890/225423346-2b9efce6-4875-4c18-809e-8bab50eea6c2.png)

After all of this, we create a function that would encompass all the steps of the transformation that we have made -

![image](https://user-images.githubusercontent.com/27859890/225424119-ec714c01-397b-415a-90b1-9c9459d876dd.png)

We now apply this function to our data and the transformations get applied to the other sheets (Rows of the table).

## Dashboarding:

After transforming our data, we load our data to Power BI Workspace.
We then use DAX Queries to create useful columns like 

1) WFH Count - Assigns 1 when the value is WFH (Work From Home) and 0.5 when the value is HWFH (Half Work From Home)

![image](https://user-images.githubusercontent.com/27859890/225424888-6e457f21-ed1f-48ff-9206-e4d609034977.png)

2) Date in MMM YY to make it easy to analyze by month - 

![image](https://user-images.githubusercontent.com/27859890/225425092-23c8e75d-f85c-4a6d-b966-2d77d8574fe7.png)


3) SL Count -  Assigns 1 when the value is SL (Sick Leave) and 0.5 when the value is HWFH (Half Sick Leave)

![image](https://user-images.githubusercontent.com/27859890/225425753-7a1532f3-416a-4606-a25f-a1e24e90fc5f.png)

4) Day of week - To make it convenient for analyze by the day of the week 

![image](https://user-images.githubusercontent.com/27859890/225426355-c2cd53f8-4156-4b42-a077-82d3818689fc.png)

We create some measures - 

Total Working Days - 

![image](https://user-images.githubusercontent.com/27859890/225428286-9ec9862a-e8e5-4d71-954d-7b96cca7c121.png)

WFH Total - 

![image](https://user-images.githubusercontent.com/27859890/225428379-4ea79bf7-d765-4c5e-839f-72547475689d.png)

WFH% - 

![image](https://user-images.githubusercontent.com/27859890/225428794-9d713dd2-fc7c-4f43-9a01-cece2590507b.png)


SL Total - 

![image](https://user-images.githubusercontent.com/27859890/225428915-28be9735-d98e-41aa-abcf-41629875966d.png)


SL% - 

![image](https://user-images.githubusercontent.com/27859890/225429023-b9b4d4dd-2bf9-4ef8-97c8-4f35676793a9.png)


Presence % - 

![image](https://user-images.githubusercontent.com/27859890/225429139-f86bc988-843b-4d76-adeb-7638f8c67206.png)

### Elements of the Dashboard:

1) Number Cards - To show summary % values of Presence, WFH, SL
2) Slicer - We have sliced our time period by months and displayed them as tiles. This enables the user to filter by month
3) Tables - We are showing 4 main tables . The first one shows summary percentage values for every employee. The second table shows detailed attendance values for every employee for every day of the chosen time period. The next two tables analyze presence% and SL% by days of the week
4) Area charts showing Presence%, WFH%, SL% by Date


### Final Dashboard - 


![image](https://user-images.githubusercontent.com/27859890/225430095-4db97fe7-1476-48e6-bc81-f121bb61aaff.png)


# Insights 

- Presence is highest in April and least in May
- WFH% is the highest in June
- Overall attendance is the highest on Tuesday, followed by Monday and Wednesday
- WFH is the highest on Fridays, followed by Thursday and then Monday

We can use these insights for,

- Project Release Planning - During client calls, we can use this historic data to decide when to work on high priority deployments or releases. Based on our data, it is preferable to make our release in April and better to avoid May. A project release is a critical event and we do not want to do it when there is a greater chance of employees going on leave or when there is general unavailibility

- Hybrid Work planning - Our data says that most employees WFH on Fridays. If we need to plan out a Hybrid set-up, we can declare Fridays and Thursdays as WFH days and the rest of the days as on-site days. This can change from month-to-month/season too.

- Resource planning - When we decide on a hybrid model, plan when employees need to attend office in person, they can cut down on expenditure like rental expenses, plan requirements of hourly wage workers on non-onsite days, cut down on electricity costs by shutting down lights, ACs in units where no employees are present on WFH days

- Plan team building, group activities - Team leads can plan leadership visits/group events on days where there is a highest probabilty of both high presence and on-site work. In this case, Tuesday is the best day to collaborate in person

## Conclusion
So far, with the data we have, we have been able to get some high level overview on the attendance patterns of employees for a duration of 3 months. This analysis can be expanded to a year or more and presence can be analyzed by seasons and holidays too. Planning for the hybrid work model is one of the many use cases of HR Analytics. We can build similar analysis for resource planning for projects to identify backup team members or help managers decide if they need to get temporary hires or contractors.








