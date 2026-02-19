# 🏗  Data & Modeling Approach
1️⃣ Data Architecture Overview

The HR analytics solution was built using a star-schema inspired dimensional model with light snowflaking for rating and satisfaction dimensions.

The model separates:
•	Fact table (transactional performance data)
•	Dimension tables (descriptive employee and classification attributes)
•	Dedicated measures table (centralized DAX logic)
This structure ensures scalability, optimized filtering behavior, and analytical flexibility.
________________________________________
# 2️⃣ Fact Table
📌 FactPerformanceRating
This table captures employee-level performance review events.
Granularity:
One row per employee per review date.
Key Columns:
•	EmployeeID
•	ReviewDate
•	EnvironmentSatisfaction
•	JobSatisfaction
•	ManagerRating
•	RelationshipSatisfaction
•	PerformanceID
This table enables:
•	Time-based review analysis
•	Rating trend tracking
•	Satisfaction pattern analysis
•	Context-aware DAX calculations
________________________________________
# 3️⃣ Dimension Tables
👤 DimEmployee
Contains static employee attributes.
Key attributes:
•	Age & AgeBins
•	Department
•	BusinessTravel
•	DistanceFromHome
•	Attrition
•	ActiveStatus
Purpose:
•	Workforce segmentation
•	Attrition analysis
•	Demographic breakdowns
•	Department-level insights
________________________________________
## 📅 DimDate
Standard calendar dimension used for time intelligence.
Includes:
•	Year
•	Month
•	FiscalMonth
•	FiscalQuarter
•	DayOfWeek
Supports:
•	Hiring trend analysis
•	Review trend analysis
•	Year-over-year comparison
•	Time-based attrition tracking
________________________________________
## 🎓 DimEducationLevel
Stores education classification data.
Enables education-level segmentation analysis.
________________________________________
## ⭐ DimRatingLevel
Separates rating category metadata from numeric values.
Improves:
•	Normalization
•	Model readability
•	Future extensibility
________________________________________
## 😊 DimSatisfiedLevel
Used for satisfaction score categorization.
Supports:
•	Employee engagement analysis
•	Satisfaction-level grouping
•	Rating interpretation
________________________________________
## 4️⃣ Modeling Design Decisions
✔ Dimensional Modeling Strategy
The model follows a star schema structure:
•	Fact table at the center
•	Dimensions filtering inward
•	Single-direction relationships (1 → many)
This design:
•	Improves query performance
•	Prevents ambiguity
•	Maintains predictable filter propagation
•	Aligns with BI best practices
________________________________________
## ✔ Relationship Strategy
•	One-to-many relationships from dimensions to fact table
•	Controlled filter direction to avoid circular dependencies
•	Dedicated Date dimension for time-based analysis
•	Inactive relationships used where alternate date logic was required (via USERELATIONSHIP())
________________________________________
## ✔ Measures Table
A separate _Measures table was created to centralize all DAX measures.
Benefits:
•	Cleaner model layout
•	Easier maintenance
•	Clear separation of logic vs structure
•	Professional BI practice
________________________________________
## 5️⃣ Granularity & Filter Context Management
Understanding granularity was critical in this project.
•	Employee-level metrics (e.g., Attrition) originate from DimEmployee
•	Review-level metrics originate from FactPerformanceRating
•	DistinctCount logic used to avoid duplication
•	Context-aware measures implemented to handle review vs employee aggregation
This ensured accurate KPI reporting across pages.
________________________________________
## 6️⃣ Advanced Techniques Used
•	Context transition with CALCULATE()
•	Alternate relationship activation using USERELATIONSHIP()
•	Dynamic KPI calculations
•	Percentage calculations with DIVIDE()
•	Conditional logic using IF() and ISBLANK()
•	Centralized DAX measure management
