# AWS CLI, S3 & Athena Setup ⚙️

This guide provides **step-by-step instructions** to configure **AWS CLI, create an S3 bucket, and run Athena queries**.

---

## 1️⃣ **AWS CLI Installation & Configuration**
1. **Install AWS CLI on Mac**:
   ```bash
   brew install awscli
   ```
2. **Install AWS CLI on Rocky Linux**:
   ```bash
   sudo dnf install awscli -y
   ```
3. **Configure AWS CLI** (Replace with your actual keys):
   ```bash
   aws configure
   ```
   - **AWS Access Key ID**: `<your-access-key>`  
   - **AWS Secret Access Key**: `<your-secret-key>`  
   - **Default region name**: `us-east-1` (or your preferred region)  
   - **Default output format**: `json`  

4. **Verify AWS CLI Configuration**:
   ```bash
   aws s3 ls
   ```

---

## 2️⃣ **S3 Bucket Setup**
1. **List your existing buckets**:
   ```bash
   aws s3 ls
   ```
2. **Create a new S3 bucket** (replace `<your_name>` with your name):
   ```bash
   aws s3 mb s3://<your_name>-vbo-de-bootcamp
   ```
3. **Upload dataset to S3**:
   ```bash
   wget https://raw.githubusercontent.com/erkansirin78/datasets/master/Churn_Modelling.csv
   aws s3 cp Churn_Modelling.csv s3://<your_name>-vbo-de-bootcamp/churn_modeling/churn_modeling.csv
   ```
4. **Verify file upload**:
   ```bash
   aws s3 ls s3://<your_name>-vbo-de-bootcamp/churn_modeling/
   ```

---

## 3️⃣ **Athena Setup**
1. **Create an Athena database**:
   ```sql
   CREATE DATABASE churn_analysis;
   ```
2. **Create an Athena table**:
   ```sql
   CREATE EXTERNAL TABLE churn_analysis.churn_data (
       RowNumber INT,
       CustomerId BIGINT,
       Surname STRING,
       CreditScore INT,
       Geography STRING,
       Gender STRING,
       Age INT,
       Tenure INT,
       Balance FLOAT,
       NumOfProducts INT,
       HasCrCard INT,
       IsActiveMember INT,
       EstimatedSalary FLOAT,
       Exited INT
   )
   ROW FORMAT SERDE 'org.apache.hadoop.hive.serde2.lazy.LazySimpleSerDe'
   WITH SERDEPROPERTIES ('serialization.format' = ',', 'field.delim' = ',')
   LOCATION 's3://<your_name>-vbo-de-bootcamp/churn_modeling/'
   TBLPROPERTIES ('skip.header.line.count'='1');
   ```

✅ **Now, AWS CLI, S3, and Athena are ready!** 