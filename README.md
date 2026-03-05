# 👥 Human Resource Analytics – Power BI  

🚀 Advanced HR Analytics Dashboard built with a robust star-schema data model  

This project delivers executive-level insights into workforce dynamics, tracking:
- Active Headcount  
- Hiring Trends  
- Employee Attrition  
- Turnover Rate  

Featuring dual date relationships (Hire & Termination), USERELATIONSHIP-based DAX calculations, and enriched employee profiling for deeper organizational insights.

🏗️ Data Model Architecture

The report follows a star schema model with the following structure:

🔹 Fact Table: FactEmployee

Contains core employee lifecycle data:

  ▫️ Hire Date
  
  ▫️ Termination Date
  
  ▫️ Birthdate
  
  ▫️ Manager
  
  ▫️ Department
  
  ▫️ Position
  
  ▫️ Education
  
  ▫️ Gender

This table drives all workforce movement calculations.

🔹 Dimension Table: DimDate

  ▫️ Active relationship → Hire Date
  
  ▫️ Inactive relationship → Termination Date

The inactive relationship is activated in DAX measures (using USERELATIONSHIP) to correctly calculate:

  ▫️ Resignations
  
  ▫️ Turnover Rate
  
  ▫️ Termination trends over time

This enables proper time-intelligence calculations for both hiring and attrition analysis.

🔹 Dimension Table: DimEmployeeProfile

Enriches employee data with:

  ▫️ Salary
  
  ▫️ Address
  
  ▫️ City
  
  ▫️ Performance Review Score

  ▫️ Picture URL

This allows deeper analytics such as:

  ▫️ Salary distribution
  
  ▫️ Performance vs Attrition insights
  
  ▫️ Geographic workforce distribution

Profile-based drill-through reporting

📈 Key Metrics Logic

  ▫️ Active Employees = CALCULATE(
      [Hires] - [Resignations],
      FILTER(
          ALL(dDate[Date]),
          dDate[Date] <= MAX(dDate[Date])
      )
  )
  
  ▫️ Hires = Count of Employees
  
  ▫️ Resignations = CALCULATE(
      COUNTROWS(fEmployee),
      fEmployee[Termination Date] <> BLANK(),
      USERELATIONSHIP(dDate[Date],fEmployee[Termination Date])
  )
  
  ▫️ Turnover Rate = Resignations / Hires

🧠 Concepts Demonstrated

  ▫️ Star Schema Modeling
  
  ▫️ Active vs Inactive Relationships
  
  ▫️ USERELATIONSHIP in DAX
  
  ▫️ Time Intelligence Calculations
  
  ▫️ Workforce Attrition Modeling
  
  ▫️ HR KPI Design Best Practices
  
  ▫️ Profile-based Data Enrichment

🎯 Purpose

This project is designed as:

  ▫️ A portfolio project for HR analytics
  
  ▫️ A demonstration of advanced Power BI modeling skills
  
  ▫️ A reusable HR reporting template
  
  ▫️ A workforce analytics showcase
