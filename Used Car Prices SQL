--(1)View the total used cars for each brand  (tableau)
select brand, count(brand) as brand_total
from cardata
group by brand
order by brand_total desc



--(2)view the total of each transmission types (tableau)
select transmission, count(transmission)
from cardata
group by transmission


--(3)View the types of cars and count how many there are (tableau)
select distinct fueltype, count(fueltype) as total
from cardata
group by fueltype
order by total desc



--(4)View how many hybrid cars does mercedes have available
select count(fueltype) as number_of_merc_hybrids
from cardata 
where brand = 'merc' and fueltype = 'Hybrid'



--(5)View how many hybrids are available for each car brand has
select brand, count(fueltype) as hybrids_available
from cardata
where fueltype = 'Hybrid'
group by brand



--(6)View how many cars each brand has based on fueltype (tableau)
select brand, fueltype, count(fueltype)
from cardata
group by brand, fueltype
order by brand, fueltype



--(7)View cars with most mpg that isn't electric, or other
select year, brand, model, fueltype, max(mpg)
from cardata
where fueltype != 'Electric' AND fueltype != 'Other' AND model != ' i3'
group by year, brand, model, fueltype
order by max(mpg) desc



--(8)get average mpg of all fueltypes (tableau)
select brand, transmission, round(avg(mpg)) as avg_mpg
from cardata
group by transmission, brand
order by brand, transmission



--(9)JOIN car data and price together and show (brand, model, mileage, and price) of each car
select brand, model, mileage, cast(price as money)
from cardata JOIN carprice 
	on cardata."carID" = carprice."carID"



--(10)View the most expensive toyotas by cost
select cardata."carID", brand, year, model, mileage, cast(max(price) as money) as price
from cardata JOIN carprice 
	on cardata."carID" = carprice."carID"
where brand = 'toyota'
group by cardata."carID", brand, year, model, mileage
order by price desc



--(11)View the price per mile for each car (tableau)
select year, brand, model, mileage, cast(price as money) as currentprice, cast(price/mileage as money) as price_per_mile
from cardata JOIN carprice 
	on cardata."carID" = carprice."carID"
order by brand, price_per_mile desc
	
	
	
--(12)View price of the most expensive car for each brand (tableau)
--listed the most max price for each brand but needed more details on the car such as (year and model) of the brand
select brand, cast(max(price) as money)
from cardata JOIN carprice 
	on cardata."carID" = carprice."carID"
group by brand
order by max(price) desc

--used a CTE with partition to help list the (year and model) of each exp car from each brand
with cardataCTE as
 (
 	select 
	 	cardata."carID", 
	    cardata.year, 
	 	brand, 
	    model, 
	 	cast(max(price) as money) as pricetag,
	    row_number() over(
			partition by
				brand
			order by 
			max(price) desc
		) rownumber
	from cardata JOIN carprice 
	    on cardata."carID" = carprice."carID"
	group by cardata."carID", cardata.year
    order by pricetag desc
 )
select year, brand, model, pricetag
from cardataCTE
where rownumber = 1











