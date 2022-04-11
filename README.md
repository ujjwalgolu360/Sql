# Sql
Some queries that I used for sales analysis of a company. For some reasons I changed the actual names of product, stores and schemas
select Product_name, coalesce(sum(Zero),0) as '2020', coalesce(sum(One), 0) as '2021', coalesce(sum(Two),0) as '2022'
from
(select Product_name,
case when year = 2020 then sum2 end as 'Zero',
case when year = 2021 then sum2 end as 'One',
case when year = 2022 then sum2 end as 'Two'
from
(select Product_name, Year, sum(sales_value) sum2
from 
(select Product_name, sales_value, case when sales_date like '2020%' then 2020
          when sales_date like '2021%' then 2021
		when sales_date like '2022%' then 2022
end as year from salesvc) a
group by Product_name, Year)b
where Year in (2020,2021,2022)
group by Product_name, year) c
group by Product_name; 
