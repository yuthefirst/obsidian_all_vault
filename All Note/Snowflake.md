### Encrypt and Decrypt
#### Encrypt
```sql
SET passphrase='thisistheprivatekey';

SELECT encrypt('Secret!', 'AAD', $passphrase);
```
#### Decrypt
```sql
SELECT
    TO_VARCHAR(
        DECRYPT(
            ENCRYPT('Secret!', 'AAD', $passphrase),
            $passphrase),
        'utf-8');
```

#### Example: 


### Snowflake with Python
- Create a role and user for snowflake connector
```sql
CREATE warehouse temp_patient_warehouse;

CREATE database temp_patient_database;

CREATE schema temp_patient_schema;

CREATE USER testing_user PASSWORD='Pass@123456' DEFAULT_ROLE = sysadmin;

GRANT ALL ON WAREHOUSE temp_patient_warehouse TO ROLE sysadmin;

GRANT ALL ON database temp_patient_database TO ROLE sysadmin;

GRANT ALL ON schema temp_patient_schema TO ROLE sysadmin;

```
- Example: Create an table and insert a CSV to that table
```python
from snowflake.connector import connect  
import csv  
from dotenv import load_dotenv  
import os  
  
# load key from .env file  
load_dotenv()  
account = os.getenv("SNOWFLAKE_TEMP_ACCOUNT")  
user = os.getenv("SNOWFLAKE_TEMP_USER")  
password = os.getenv("SNOWFLAKE_TEMP_PASSWORD")  
warehouse = os.getenv("SNOWFLAKE_TEMP_WAREHOUSE")  
database = os.getenv("SNOWFLAKE_TEMP_DATABASE")  
schema = os.getenv("SNOWFLAKE_TEMP_SCHEMA")  
  
  
# Snowflake connection settings  
conn = connect(  
account=account,  
user=user,  
password=password,  
warehouse=warehouse,  
database=database,  
schema=schema  
)  
  
  
# Establish connection to Snowflake  
cursor = conn.cursor()  
  
# Create table  
create_table_sql = """  
CREATE TABLE IF NOT EXISTS patients (  
patient_id INTEGER,  
name VARCHAR,  
dob DATE,  
address VARCHAR,  
phone VARCHAR  
)  
"""  
cursor.execute(create_table_sql)  
  
# Read data from CSV file  
filename = 'fake_patient_data.csv'  
with open(filename, 'r') as csvfile:  
reader = csv.reader(csvfile)  
next(reader) # Skip header row  
for row in reader:  
patient_id, name, dob, address, phone = row  
insert_statement = f"INSERT INTO patients VALUES ({patient_id}, '{name}', '{dob}', '{address}', '{phone}')"  
cursor.execute(insert_statement)  
  
# Close the connection  
cursor.close()  
conn.close()  
  
print("Data inserted into Snowflake table")

```
