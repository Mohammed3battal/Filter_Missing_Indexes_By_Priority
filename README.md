## Script: Get_Missing_Indexes_With_Recommendation_priorityLevel.sql

**Description**:
This script retrieves detailed missing index suggestions from SQL Server DMVs and categorizes them into **priority levels** based on usage frequency, estimated performance gain, and query resource cost. It also includes SQL Server uptime context and generates ready-to-execute `CREATE INDEX` statements.

---

### Key Features:
- Calculates a composite **improvement score**
- Shows **last SQL Server restart** and **days since**
- Assigns **index recommendation levels**:
  - `High Priority`
  - `Medium Priority`
  - `Low Priority`
  - `Ignore`
- Dynamically builds `CREATE INDEX` scripts
- Fully filterable by:
  - Priority level
  - Query cost
  - Specific database

---

### Output Columns:

| Column                                 | Description                                               |
|----------------------------------------|-----------------------------------------------------------|
| `Current_Run_Time`                     | Execution timestamp                                       |
| `SQL_Server_Last_Startup`              | Last SQL Server startup time                              |
| `Days_Since_Last_Restart`              | DMV data freshness reference                              |
| `Database_Name`                        | The database affected by the missing index                |
| `Avg_ResourceCost_Without_Index`       | Average estimated query cost without the index            |
| `Estimated_Performance_Improvement_Percentage` | Query performance gain estimate                |
| `Number_of_Times_This_Code_Was_Executed` | Usage frequency across execution plans               |
| `Estimated_Improvement_Score`          | Combined metric: Cost × Impact × Frequency                |
| `Index_Recommendation_Level`           | Decision support: High, Medium, Low, or Ignore            |
| `Create_Index_Statement`               | T-SQL to create the recommended index                     |

---

### Optional Filters:
Uncomment the below to refine output:
```sql
--WHERE 
-- Index_Recommendation_Level = 'High Priority'
-- AND Avg_ResourceCost_Without_Index > 5
-- AND Database_Name = 'YourDatabaseName'
```

---

### Use Cases:
- Focus only on **high-impact index opportunities**
- Support **index review meetings** with metrics and justifications
- Log and track **missing index patterns** over time

