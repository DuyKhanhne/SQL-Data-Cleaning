# SQL-Data-Cleaning
This is an educational project on data cleaning and preparation using SQL. The original database in CSV format is located in the file club_member_info.csv. Here, we will explore the steps that need to be applied to obtain a cleansed version of the dataset.

Let's inspect the initial rows to analyze the data in its original format.

**Code**
Select*from club_member_info
limit 10;

**The result:**
|full_name|age|martial_status|email|phone|full_address|job_title|membership_date|
|---------|---|--------------|-----|-----|------------|---------|---------------|
|addie lush|40|married|alush0@shutterfly.com|254-389-8708|3226 Eastlawn Pass,Temple,Texas|Assistant Professor|7/31/2013|
|      ROCK CRADICK|46|married|rcradick1@newsvine.com|910-566-2007|4 Harbort Avenue,Fayetteville,North Carolina|Programmer III|5/27/2018|
|Sydel Sharvell|46|divorced|ssharvell2@amazon.co.jp|702-187-8715|4 School Place,Las Vegas,Nevada|Budget/Accounting Analyst I|10/6/2017|
|Constantin de la cruz|35||co3@bloglines.com|402-688-7162|6 Monument Crossing,Omaha,Nebraska|Desktop Support Technician|10/20/2015|
|  Gaylor Redhole|38|married|gredhole4@japanpost.jp|917-394-6001|88 Cherokee Pass,New York City,New York|Legal Assistant|5/29/2019|
|Wanda del mar       |44|single|wkunzel5@slideshare.net|937-467-6942|10864 Buhler Plaza,Hamilton,Ohio|Human Resources Assistant IV|3/24/2015|
|Joann Kenealy|41|married|jkenealy6@bloomberg.com|513-726-9885|733 Hagan Parkway,Cincinnati,Ohio|Accountant IV|4/17/2013|
|   Joete Cudiff|51|divorced|jcudiff7@ycombinator.com|616-617-0965|975 Dwight Plaza,Grand Rapids,Michigan|Research Nurse|11/16/2014|
|mendie alexandrescu|46|single|malexandrescu8@state.gov|504-918-4753|34 Delladonna Terrace,New Orleans,Louisiana|Systems Administrator III|3/12/1921|
| fey kloss|52|married|fkloss9@godaddy.com|808-177-0318|8976 Jackson Park,Honolulu,Hawaii|Chemical Engineer|11/5/2014|

**Cleaning data steps:**

**Step 1:** Create a new table for cleaning by generating a new table where I manipulate and restructure the data without modifying the original dataset. 

    CREATE TABLE club_member_info_cleaned (
		full_name VARCHAR(50),
		age INTEGER,
		martial_status VARCHAR(50),
		email VARCHAR(50),
		phone VARCHAR(50),
		full_address VARCHAR(50),
		job_title VARCHAR(50),
		membership_date VARCHAR(50)
    ;

Then copy all values from the original table.

    INSERT INTO club_member_info_cleaned
	SELECT*FROM club_member_info
    ;
**Step 2:** Fix structural errors such as typos. trim values, and incorrect capitalization in the first column _full_name_.

    UPDATE club_member_info_cleaned
	SET full_name = TRIM(UPPER(full_name));
    UPDATE club_member_info_cleaned 
	SET full_name = 
		CASE WHEN full_name = ' ' THEN NULL
		ELSE full_name 
	END;

**Step 3:** Fix wrong values in _Age_. To check the problem in this column, I used sorting tools to determine the wrong values.
    
    UPDATE club_member_info_cleaned 
	SET age =
		CASE WHEN age = ' ' THEN NULL 
		WHEN age > 70 THEN NULL 
		ELSE age 
	END; 
 
 **Step 4:** First check the values in the column _martial_status_ by using group by. There are some trim values and typos errors. Then I can fix the problems.
    
    UPDATE club_member_info_cleaned
    SET martial_status = CASE
	WHEN martial_status ='' THEN NULL 
	WHEN martial_status ='divored' THEN 'divorced'
	ELSE martial_status
    END;

**Step 5:** Fix the blank value in the email column.

    UPDATE club_member_info_cleaned 
    SET email = NULL 
    WHERE email = '';

**Step 6:** Fix the blank values in the column phone.

    UPDATE club_member_info_cleaned 
    SET phone = NULL 
    WHERE phone = '';

**Step 7:** Fix blank values in _Job title_.

    UPDATE club_member_info_cleaned 
    SET job_title = NULL 
    WHERE job_title = '';

THAT'ALL! NOW WE HAVE A CLEARED DATABASE.










