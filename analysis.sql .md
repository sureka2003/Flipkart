

**Find the most popular product based on total quantity sold in 2023\.**

select s.order\_id,s.product\_id,p.product\_name,   
sum(s.quantity)  
from sales as s  
join products as p on s.product\_id=p.product\_id  
where Extract (year from order\_date)=2023  
group by s.order\_id,s.product\_id,p.product\_name  
order by sum(s.quantity) DESC  
Limit 1;

**Get the count of returned orders by shipping provider in 2023\.**

select shipping\_providers,  
count(order\_id)  
from shippings   
where delivery\_status \= 'Returned '  
and extract (year from return\_date) \= 2023  
group by shipping\_providers

**Show the total revenue generated per month for the year 2023\.**

select To\_CHAR(order\_date,'Month') AS month\_name,  
sum (quantity\*price\_per\_unit) as total\_revenue  
from sales   
where extract(year from order\_date) \= 2023  
and order\_status \= 'Completed'  
group by To\_CHAR(order\_date,'Month')  
order by sum (quantity\*price\_per\_unit) DESC

**Find the customers who have made the most purchases in a single month.**

select c.customer\_id,TO\_CHAR(order\_date,'Month'),  
count( s.order\_id)  
from sales as s  
Join customers as c on c.customer\_id \= s.customer\_id  
group by c.customer\_id,TO\_CHAR(order\_date,'Month')  
order by count(s.order\_id) DESC  
Limit 1;

**Retrieve the number of orders made per product category in 2023     and order by total quantity sold.**

select p.category,  
count(s.order\_id)  
from sales as s  
join products as p on p.product\_id \= s.product\_id  
where extract(year from s.order\_date)= 2023  
group by p.category  
order by count(s.order\_id) DESC

**MEDIUM TO ADVANCED QUERIES:**  

**Get a list of all customers who have placed orders, including those with no payment records.** 

select c.customer\_id,c.customer\_name,p.payment\_id  
from customers as c   
left join sales as s on s.customer\_id \= c.customer\_id  
full join payments as  p on p.order\_id \= s.order\_id

**Retrieve products ordered by customers who are in the 'Gujarat' state and whose total order price is greater than 15,000**

select s.product\_id,  
sum (s.quantity \* s.price\_per\_unit) as total\_price  
from sales as s  
join customers as c on c.customer\_id \= s.customer\_id  
where state \= 'Gujarat'  
group by s.product\_id  
Having sum(s.quantity \* s.price\_per\_unit) \> 15000

**Retrieve the total sales per customer in 'Delhi' where the order status is 'Completed',only include those with total sales greater than 50,000 and order the results by total sales.**

select s.customer\_id,c.customer\_name,  
sum(s.quantity \* s.price\_per\_unit)  
from sales as s  
join customers as c on c.customer\_id \= s.customer\_id   
where c.state \= 'Delhi'  
and s.order\_status \= 'Completed'  
group by s.customer\_id,c.customer\_name  
Having sum(s.quantity \* s.price\_per\_unit) \> 50000  
order by sum(s.quantity \* s.price\_per\_unit) DESC

**Show the total quantity sold per product in the 'Accessories' category where the total quantity sold is greater than 50 and order the results by product name**

select s.product\_id,p.product\_name,  
sum(s.quantity) as total\_quantity  
from sales as s  
join products as p on p.product\_id \= s.product\_id  
where p.category \= 'Accessories'  
group by s.product\_id,p.product\_name  
Having sum(s.quantity) \> 50  
order by p.product\_name

**Get a list of all customers who have placed orders, including those with no payment records.** 

select c.customer\_id,c.customer\_name,p.payment\_id  
from customers as c   
left join sales as s on s.customer\_id \= c.customer\_id  
full join payments as  p on p.order\_id \= s.order\_id

**Get the top 5 customers by total spending on 'Accessories'.** 

select s.customer\_id,c.customer\_name,  
sum(s.quantity\*s.price\_per\_unit)  
from sales as s  
join customers as c on c.customer\_id \= s.customer\_id  
join products as p on p.product\_id \= s.product\_id  
where p.category \= 'Accessories'  
group by s.customer\_id,c.customer\_name  
order by sum(s.quantity\*s.price\_per\_unit) DESC  
Limit 5 

