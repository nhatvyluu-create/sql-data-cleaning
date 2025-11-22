# sql-data-cleaning
This is an educational project on data cleaning and preparation using SQL. The original database in CSV format is located in the file club_member_info.csv. Here, we will explore the steps that need to be applied to obtain a cleansed version of the dataset.
## Data Overview
Query to show overview data:
```sql
SELECT * FROM club_member_info cmi
LIMIT 10:
```
Result:
|full_name|age|martial_status|email|phone|full_address|job_title|membership_date|
|---------|---|--------------|-----|-----|------------|---------|---------------|
|ADDIE LUSH|40|married|alush0@shutterfly.com|254-389-8708|3226 Eastlawn Pass,Temple,Texas|Assistant Professor|7/31/2013|
|ROCK CRADICK|46|married|rcradick1@newsvine.com|910-566-2007|4 Harbort Avenue,Fayetteville,North Carolina|Programmer III|5/27/2018|
|SYDEL SHARVELL|46|divorced|ssharvell2@amazon.co.jp|702-187-8715|4 School Place,Las Vegas,Nevada|Budget/Accounting Analyst I|10/6/2017|
|CONSTANTIN DE LA CRUZ|35|Unknown Status|co3@bloglines.com|402-688-7162|6 Monument Crossing,Omaha,Nebraska|Desktop Support Technician|10/20/2015|
|GAYLOR REDHOLE|38|married|gredhole4@japanpost.jp|917-394-6001|88 Cherokee Pass,New York City,New York|Legal Assistant|5/29/2019|
|WANDA DEL MAR|44|single|wkunzel5@slideshare.net|937-467-6942|10864 Buhler Plaza,Hamilton,Ohio|Human Resources Assistant IV|3/24/2015|
|JOANN KENEALY|41|married|jkenealy6@bloomberg.com|513-726-9885|733 Hagan Parkway,Cincinnati,Ohio|Accountant IV|4/17/2013|
|JOETE CUDIFF|51|divorced|jcudiff7@ycombinator.com|616-617-0965|975 Dwight Plaza,Grand Rapids,Michigan|Research Nurse|11/16/2014|
|MENDIE ALEXANDRESCU|46|single|malexandrescu8@state.gov|504-918-4753|34 Delladonna Terrace,New Orleans,Louisiana|Systems Administrator III|3/12/1921|
|FEY KLOSS|52|married|fkloss9@godaddy.com|808-177-0318|8976 Jackson Park,Honolulu,Hawaii|Chemical Engineer|11/5/2014|

###  Create a copy of club member table
Query
```sql
CREATE TABLE club_member_info_cleaned (
	full_name VARCHAR(50),
	age INTEGER,
	martial_status VARCHAR(50),
	email VARCHAR(50),
	phone VARCHAR(50),
	full_address VARCHAR(50),
	job_title VARCHAR(50),
	membership_date VARCHAR(50)
);
```
Query to transfer data from old table to new table
```sql
INSERT INTO club_member_info_cleaned
SELECT * FROM club_member_info;
```
Query to capitalize name
```sql
UPDATE club_member_info_cleaned
SET full_name = UPPER(TRIM(full_name));
```
Query to fill NULL values in martial status with 'Unknow Status' 
```sql
UPDATE club_member_info_cleaned 
SET martial_status = 'Unknown Status'
WHERE martial_status = '';
```
Query to find if there are NULL values or not logical (age >=100) values in age 
```sql
SELECT * FROM club_member_info_cleaned cmic WHERE AGE IS NULL or AGE > 100;
```
Query to change NULL or not logical values in age to median value of that column
```sql
UPDATE club_member_info_cleaned
SET age = (SELECT Median(age) FROM club_member_info_cleaned)
WHERE age IS NULL or age >100;
```
Query to check NULL values of phone column
```sql
SELECT * FROM club_member_info_cleaned WHERE phone IS NULL OR phone = ''
```
Query to fill NULL values in phone with 'Unknown Phone Number' 
```sql
UPDATE club_member_info_cleaned
SET phone = 'Unknown Phone Number'
WHERE phone = '';
```
Query to check NULL values of job_title
```sql
SELECT * FROM club_member_info_cleaned WHERE job_title IS NULL OR job_title = '';
```
Query to fill NULL values in job_title with 'Unknown Job Title'
```sql
UPDATE club_member_info_cleaned
SET job_title = 'Unknown Job Title'
WHERE job_title = '';
