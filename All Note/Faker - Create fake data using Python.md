This library is using to create the Fake data:
- Install Faker
```python
pip install Faker
```
- Generate fake data and save it to a CSV file
```python

import csv

from faker import Faker

​

# Create Faker object

fake = Faker()

​

# Generate fake patient data

data = []

for _ in range(10):

    patient_id = fake.unique.random_number(digits=6)

    name = fake.name()

    dob = fake.date_of_birth(minimum_age=18, maximum_age=90).strftime("%Y-%m-%d")

    address = fake.address().replace("\n", ", ")

    phone = fake.phone_number()

    data.append([patient_id, name, dob, address, phone])

​

# Save data to CSV file

filename = 'fake_patient_data.csv'

with open(filename, 'w', newline='') as csvfile:

    writer = csv.writer(csvfile)

    writer.writerow(['Patient ID', 'Name', 'Date of Birth', 'Address', 'Phone'])

    writer.writerows(data)

​

print(f"Fake patient data saved to {filename}")

```
In this updated code, we've added extra fields relevant to optometry patient data, such as `Patient ID`, `Date of Birth`, and `Address`. We generate a unique patient ID using the `random_number()` method to ensure uniqueness. The date of birth is generated using the `date_of_birth()` method with a minimum age of 18 and a maximum age of 90. The patient's address is generated using the `address()` method, and the newline character is replaced with a comma for proper formatting.

The rest of the code remains the same as before, where the data is saved to a CSV file named `fake_patient_data.csv`, and a message is printed to confirm the location of the saved file.


- We also can populate a [[Snowflake#Snowflake with Python]] table with this fake data

```[!Warning]
```

[>]

