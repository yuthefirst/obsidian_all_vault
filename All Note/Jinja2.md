### 1. Using Jinja2 in the [[DBT#Macro]]
- Example 1:
```sql
-- models/orders.sql
{% set source_name = 'jaffle_shop' %}

select ...
from {{ ref('ingest_OPTOMATE_' ~ source_name ~ '_PATIENT') }}
```
In this example, using ~ to combine 2 string with an argument

- Example 2:
```sql
-- models/orders.sql
{% set source_name = 'jaffle_shop' %}
{% set table_name = 'orders' %}

select ...
from {{ source(source_name, table_name) }}
left join {{ source(source_name, 'customers') }} using (customer_id)
where order_date >= '{{ start_date }}'
```
In dbt, you can use `{{ }}` to insert the value of a variable or expression into the middle of a string using Jinja templating. The content inside the `{{ }}` is evaluated as a Jinja expression and the result is inserted into the string at that position.

