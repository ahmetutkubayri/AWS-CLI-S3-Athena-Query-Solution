# Churn Ratio Calculation in Athena 🚀

This document explains how to **run an Athena query to calculate customer churn ratio.**

---

## **1️⃣ Data Preparation**
- **Dataset is uploaded to S3:**
  ```bash
  aws s3 cp Churn_Modelling.csv s3://<your_name>-vbo-de-bootcamp/churn_modeling/churn_modeling.csv
  ```
- **Athena table `churn_analysis.churn_data` is created.**

---

## **2️⃣ Run Athena Query to Get Churn Ratio**
1. **Open Athena Query Editor**.
2. **Execute the following query**:
   ```sql
   SELECT 
       COUNT(CASE WHEN Exited = 1 THEN 1 END) AS exited_one_count,
       COUNT(CASE WHEN Exited = 0 THEN 1 END) AS exited_zero_count,
       CAST(COUNT(CASE WHEN Exited = 1 THEN 1 END) AS DOUBLE) / COUNT(*) AS leaving_ratio
   FROM churn_analysis.churn_data;
   ```

---

## **3️⃣ Expected Query Result**
```commandline
#	exited_one_count	exited_zero_count	leaving_ratio
1	2037.0	            7963.0	            0.25580811252040686
```

✅ **Final Result: We successfully calculated the churn ratio using AWS Athena!** 