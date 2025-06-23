## Workforce Analytics with DAX in Power BI

This project is a detailed demonstration of workforce analytics using Power BI with a star schema data model. 
It includes four dimension tables and one fact table. 
Using DAX functions, I derived actionable insights, KPIs, and visualizations for HR and operational decision-making.

---

### DAX functions for Workforce Analytics

![DAX functions for staff data analysis](https://github.com/user-attachments/assets/c382740d-a4e6-4342-82c8-d15b78670ddc)


## 📈 Data Model

### 1. **Fact Table:**
#### `FactEmployeePerformance`
- `EmployeeID`
- `DepartmentID`
- `RoleID`
- `LocationID`
- `Date`
- `WorkHours`
- `TasksCompleted`
- `ErrorsMade`
- `Salary`

### 2. **Dimension Tables:**
#### `DimEmployee`
- `EmployeeID`
- `FirstName`
- `LastName`
- `Gender`
- `Age`
- `HireDate`

#### `DimDepartment`
- `DepartmentID`
- `DepartmentName`
- `ManagerID`

#### `DimRole`
- `RoleID`
- `RoleName`
- `SeniorityLevel`

#### `DimLocation`
- `LocationID`
- `City`
- `Country`

---

## 💡 Business Problems & DAX Solutions

### 1. **Average Work Hours Per Department**
```dax
AvgWorkHoursPerDept = 
AVERAGEX(
    VALUES(DimDepartment[DepartmentName]),
    CALCULATE(SUM(FactEmployeePerformance[WorkHours]))
)
```
Insight: Helps compare average working hours across departments. 
This can highlight departments where staff might be overworked, underutilized, or optimally staffed.

### 2. **Employee Efficiency Score**

```dax
EfficiencyScore = 
DIVIDE(
    SUM(FactEmployeePerformance[TasksCompleted]),
    SUM(FactEmployeePerformance[WorkHours])
)
```
Insight: Measures how efficiently employees complete tasks based on time spent. 
It can assist in identifying top performers and potential productivity gaps.

### 3. **Average Salary by Role**

```dax
AvgSalaryByRole = 
CALCULATE(
    AVERAGE(FactEmployeePerformance[Salary]),
    ALLEXCEPT(DimRole, DimRole[RoleName])
)
```

Insight: Evaluates average compensation per role, helping HR assess pay parity and 
compensation alignment across job functions.


### 4. **Error Rate by Department**

```dax
ErrorRate = 
DIVIDE(
    SUM(FactEmployeePerformance[ErrorsMade]),
    SUM(FactEmployeePerformance[TasksCompleted])
)
```
Insight: Calculates how often errors are made relative to completed tasks. 
This metric can guide training needs or identify process inefficiencies in specific departments.


### 5. **Tenure of Employee**

```dax
Tenure = 
DATEDIFF(DimEmployee[HireDate], TODAY(), YEAR)
```

Insight: Measures how long each employee has been with the company. 
This helps in understanding employee retention trends and recognizing long-tenured staff.



![Staff Data Visualization](https://github.com/user-attachments/assets/181a4835-c873-4ba7-a9e1-12b958ade452)




![Staff Data Analysis](https://github.com/user-attachments/assets/a43f57d8-9899-431d-b5e6-843203ca6285)



#### This Power BI project demonstrates how DAX can be applied to workforce-related data for generating meaningful HR and operational insights. The metrics and modeling in this report serve as a strong portfolio piece for any data analyst focused on people analytics or business intelligence.


