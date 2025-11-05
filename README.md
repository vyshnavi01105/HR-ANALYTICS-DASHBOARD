# 🧠 HR Analytics Power BI Dashboard

## 📄 Overview
This project presents a **Power BI HR Analytics Dashboard** designed to help organisations monitor, analyse, and optimise workforce data.  
The dashboard offers **interactive visualisations** for KPIs such as employee attrition, diversity, salary, and performance—empowering HR teams to make data-driven decisions.

---

## 📊 Dataset
Imported CSV data files:
- `Employee_Data.csv`
- `Attrition_Data.csv`
- `Department_Data.csv`

### Fields Used
- EmployeeID, Name, Age, Gender, Department  
- Education, JobRole, Experience, PerformanceRating  
- MonthlyIncome, Attrition, MaritalStatus, Tenure  

---

## 🧹 Data Transformation
All cleaning and transformations were performed in **Power Query**:
- Removed duplicates and null values  
- Standardised categorical fields (e.g., “Sales” vs “sales”)  
- Created calculated columns for:
  - `AgeGroup` → 20–30 / 31–40 / 41–50 / 50+  
  - `ExperienceLevel` → Beginner / Intermediate / Expert  
  - `SalaryBand` → Low / Medium / High  
- Converted date fields into *Year-Month* format for time-series analysis  

---

## 🧩 Data Model
**Tables:**
- `Employee_Data` (Primary Key: EmployeeID)
- `Attrition_Data` (Linked via EmployeeID)
- `Department_Data` (Linked via DepartmentName)

**Relationships:** One-to-many between Department and Employee tables.

### ⚙️ DAX Measures
```DAX
Total Employees = COUNT(Employee_Data[EmployeeID])
Active Employees = CALCULATE(COUNT(Employee_Data[EmployeeID]), Employee_Data[Attrition] = "No")
Attrition Count = CALCULATE(COUNT(Employee_Data[EmployeeID]), Employee_Data[Attrition] = "Yes")
Attrition Rate (%) = DIVIDE([Attrition Count], [Total Employees]) * 100
Average Salary = AVERAGE(Employee_Data[MonthlyIncome])
Average Experience = AVERAGE(Employee_Data[TotalWorkingYears])



Attrition by Department =
CALCULATE(COUNT(Employee_Data[EmployeeID]), Employee_Data[Attrition] = "Yes", VALUES(Employee_Data[Depa