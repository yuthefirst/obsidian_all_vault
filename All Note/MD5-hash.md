Using MD5-hash to hash the file and return to hex decimal

```python  
import hashlib  
import os

def dump_md5(directory, extension):    
	for root, _, files in os.walk(directory):  
	        for file in files:  
	            md5_hash = hashlib.md5()  
	            if file.endswith(extension):  
	                file_path = os.path.join(root, file)  
	                with open(file_path, 'rb') as f:  
	                    while True:  
	                        data = f.read(8192)  # Read the file in chunks  
	                        if not data:  
	                            break  
	                        md5_hash.update(data)  
	                print(file_path)  
	                print(md5_hash.hexdigest())directory_path = './models'  
file_extension = '.sql.gen'  
dump_md5(directory_path, file_extension)  
``` 
- Example:
```bash
$ python md5-hash.py  
./models/datavault/stage/stage_2_hashdiff/optomate/stage_optomate_2000_060_patient.sql.gen  
f901d2693bcd1c7994821908d553cfa4  
./models/datavault/stage/stage_1_pre/sales_force/pre_stage_sales_force_${SOURCE_ID}_ticket.sql.gen  
a92959122417b6e4641d1f667fc4857d  
./models/datavault/stage/stage_1_pre/optomate/pre_stage_optomate_${SOURCE_ID}_patient.sql.gen  
6cfbd0c3c268cdbbfeb92e76b81e9514
```

