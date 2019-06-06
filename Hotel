1. Guest 1183. Give the booking_date and the number of nights for guest 1183.

select booking_date, nights
from booking
where guest_id = 1183;



2. When do they get here? List the arrival time and the first and last names for all guests due to arrive on 2016-11-05, order the output by time of arrival.

select booking.arrival_time, guest.first_name, guest.last_name
from booking
join guest
on booking.guest_id = guest.id
where YEAR(booking.booking_date) = '2016'
	    AND MONTH(booking.booking_date) = '11'
	    AND DAY(booking.booking_date) = '05'
order by booking.arrival_time;



3. Look up daily rates. Give the daily rate that should be paid for bookings with ids 5152, 5165, 5154 and 5295. Include booking id, room type, number of occupants and the amount.

SELECT booking.booking_id, booking.room_type_requested, booking.occupants, rate.amount
FROM booking
JOIN rate
ON (booking.occupants = rate.occupancy
AND booking.room_type_requested = rate.room_type)
WHERE booking.booking_id = 5152
	    OR booking.booking_id = 5154
	    OR booking.booking_id = 5295;




4. Edinburgh Residents. For every guest who has the word “Edinburgh” in their address show the total number of nights booked. Be sure to include 0 for those guests who have never had a booking. Show last name, first name, address and number of nights. Order by last name then first name.

SELECT g.last_name, g.first_name, g.address,
	CASE WHEN SUM(booking.nights) IS NULL THEN 0
		ELSE SUM(booking.nights) END AS nights
FROM booking

RIGHT JOIN guest g
ON (g.id = booking.guest_id)
WHERE g.address LIKE '%Edinburgh%'
GROUP BY g.last_name, g.first_name, g.address
ORDER BY g.last_name, g.first_name;




5 . Show the number of people arriving. For each day of the week beginning 2016-11-25 show the number of people who are arriving that day.

SELECT booking_date AS i, COUNT(booking_id) AS arrivals
FROM booking
WHERE booking_date BETWEEN '2016-11-25' AND '2016-12-01'
GROUP BY booking_date;




6. Check out per floor. The first digit of the room number indicates the floor – e.g. room 201 is on the 2nd floor. For each day of the week beginning 2016-11-14 show how many guests are checking out that day by floor number. Columns should be day (Monday, Tuesday ...), floor 1, floor 2, floor 3.

SELECT DATE_ADD(booking_date, INTERVAL nights DAY) , SUM(CASE WHEN room_no LIKE '1%' THEN 1 ELSE 0 END) AS 1st, SUM(CASE WHEN room_no LIKE '2%' THEN 1 ELSE 0 END) AS 2nd, SUM(CASE WHEN room_no LIKE '3%' THEN 1 ELSE 0 END) AS 3rd
FROM booking
WHERE DATE_ADD(booking_date, INTERVAL nights DAY) BETWEEN '2016-11-14' AND '2016-11-20'
GROUP BY DATE_ADD(booking_date, INTERVAL nights DAY);




7. Gross income by week. Money is collected from guests when they leave. For each Thursday in November show the total amount of money collected from the previous Friday to that day, inclusive.

SELECT DATE_ADD(MAKEDATE(2016, 7), INTERVAL WEEK(DATE_ADD(booking.booking_date, INTERVAL booking.nights - 5 DAY), 0) WEEK) AS i,
	SUM(booking.nights * rate.amount) + SUM(e.amount) AS Total
FROM
	booking
	JOIN
		rate
		ON (booking.occupants = rate.occupancy
		AND booking.room_type_requested = rate.room_type)
	LEFT JOIN
		(SELECT booking_id, SUM(amount) as amount
		 FROM extra
		 group by booking_id)  AS e
	ON (e.booking_id = booking.booking_id)
  GROUP BY 1;
  
  
  
  
8. When do they get here? List the arrival time and the first and last names for all guests due to arrive on 2016-11-05, order the output by time of arrival.

select booking.arrival_time, guest.first_name, guest.last_name
from booking
join guest
on (booking.guest_id = guest.id)
where YEAR(booking.booking_date) = '2016'
	    AND MONTH(booking.booking_date) = '11'
	    AND DAY(booking.booking_date) = '05'
order by booking.arrival_time;


