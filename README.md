# Workforce Analytics with DAX in Power BI

This project is a detailed demonstration of workforce analytics using Power BI with a star schema data model. 
It includes four dimension tables and one fact table. 
Using DAX functions, I derived actionable insights, KPIs, and visualizations for HR and operational decision-making.

---

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


EfficiencyScore = 
DIVIDE(
    SUM(FactEmployeePerformance[TasksCompleted]),
    SUM(FactEmployeePerformance[WorkHours])
)

