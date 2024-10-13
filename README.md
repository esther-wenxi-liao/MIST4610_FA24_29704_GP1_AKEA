# Team name and members
**Team name:**

AKEA


**Members:**

1. Andrew Hancock @AndyH775
2. Kaniyah McGee @Kmcgee2026
3. Esther Liao @esther-wenxi-liao
4. Alexis Williams ​

# Project Scenario

At Atlanta’s Hartsfield-Jackson Airport, hundreds of flights land and take off every day, and the airport needs to:​

- Track flights arriving from and departing to various destinations.​

- Assign terminal gates to each flight.​

- Monitor crew members and airport staff working at the airport.​

- Verify that the appropriate employees are certified for certain plane before assigning them to a flight.​

- Manage passenger flow efficiently through ticketing and boarding.​


Our project simulates how an airport can manage these operational complexities through a well-designed database system that tracks and organizes flight-related information.​


The data comprises a sampling of domestic flights coming in and out of Atlanta's Hartsfield-Jackson Airport on October 3, 2024 along with associated airline and plane data.​


# Data Model

![Final Draft Model](https://github.com/user-attachments/assets/1c8f733e-3459-4f55-b031-0f3bc2d4d5d9)

# Data Dictionary

<img width="1253" alt="Screenshot 2024-10-13 at 3 18 32 PM" src="https://github.com/user-attachments/assets/f71c3129-5040-48fb-8cbe-c728f3668291">

<img width="1400" alt="Screenshot 2024-10-13 at 2 59 34 PM" src="https://github.com/user-attachments/assets/867b5915-9178-43f1-bebb-750e38c898c3">

<img width="1400" alt="Screenshot 2024-10-13 at 3 00 08 PM" src="https://github.com/user-attachments/assets/b215952a-e9dd-43df-827a-bd7364997806">

<img width="1400" alt="Screenshot 2024-10-13 at 3 00 34 PM" src="https://github.com/user-attachments/assets/7af797bf-164d-4095-ad38-47bd9454fb13">

<img width="1400" alt="Screenshot 2024-10-13 at 2 52 53 PM" src="https://github.com/user-attachments/assets/ccceb881-c990-4f60-8cc0-e1ea314c208a">

<img width="1400" alt="Screenshot 2024-10-13 at 2 53 22 PM" src="https://github.com/user-attachments/assets/867c7ec1-eb22-41ab-a215-794c8f974b09">

<img width="1400" alt="Screenshot 2024-10-13 at 2 53 49 PM" src="https://github.com/user-attachments/assets/5cd23ae8-4ffd-47f0-a04a-9fc647e719c4">

<img width="1400" alt="Screenshot 2024-10-13 at 2 58 03 PM" src="https://github.com/user-attachments/assets/b92a7c2f-e11d-4457-bde4-0d8d8aeb76a0">

<img width="1400" alt="Screenshot 2024-10-13 at 2 56 55 PM" src="https://github.com/user-attachments/assets/3d985a74-25fb-4987-8251-0bd5e442cd17">

<img width="1400" alt="Screenshot 2024-10-13 at 2 57 16 PM" src="https://github.com/user-attachments/assets/e1cf702f-1544-4677-98fb-6e3127a835d5">

<img width="1400" alt="Screenshot 2024-10-13 at 2 57 37 PM" src="https://github.com/user-attachments/assets/b99a2eb9-177e-43da-b57c-e221a992fe91">


# Ten Queries

1. Find the total number of flights for each airline with planes that are 10 years and older

```ruby
SELECT 
    airlineName, COUNT(flightNum) AS NumofFlights
FROM
    Airline,
    Plane,
    Flight
WHERE
    Airline.airlineCode = Plane.airlineCode
        AND Plane.planeRegistrationNum = Flight.planeRegistrationNum
        AND planeAge >= 10
GROUP BY airlineName; 
```


2. Grouped by airline, terminal, and calculate the occupancy rate and revenue for each flight​

```ruby
SELECT 
    Flight.flightNum,
    Flight.terminal,
    Airline.airlineName,
    Airline.airlineCode,
    COUNT(DISTINCT Ticket.idPassenger) / PlaneModel.capacity * 100 AS occupancyRate,
    SUM(Ticket.ticketPrice) AS totalRevenue
FROM
    Flight
        JOIN
    Ticket ON Flight.flightNum = Ticket.flightNum
        JOIN
    Plane ON Flight.planeRegistrationNum = Plane.planeRegistrationNum
        JOIN
    Airline ON Plane.airlineCode = Airline.airlineCode
        JOIN
    PlaneModel ON Plane.modelName = PlaneModel.modelName
GROUP BY Flight.flightNum , Flight.terminal , Airline.airlineName , Airline.airlineCode , PlaneModel.capacity;
```


3. Retrieve all Pilot's names who are currently working for Delta Air Lines with at least 8,000 flight hours. List results in alphabetical order.​

```ruby
SELECT 
    Employee.empFName, Employee.empLName, Employee.flightHour
FROM
    Employee
        JOIN
    EmployeeContract ON EmployeeContract.idEmployee = Employee.idEmployee
        JOIN
    Airline ON EmployeeContract.airlineCode = Airline.airlineCode
WHERE
    Airline.airlineName = 'Delta Air lines'
        AND Employee.position = 'Pilot'
        AND Employee.flightHour >= 1000
ORDER BY Employee.empLName DESC;
```


4. Ensure that all crew members on each flight are certified for the plane model they are assigned to, ensuring compliance. 

```ruby
SELECT 
    Flight.flightNum,
    CASE
        WHEN
            COUNT(*) = COUNT(CASE
                WHEN Certificate.modelName = PlaneModel.modelName THEN 1
            END)
        THEN 1
        ELSE 0
    END AS allCertified
FROM
    Flight
        JOIN
    AirCrew ON Flight.flightNum = AirCrew.flightNum
        JOIN
    Employee ON AirCrew.idEmployee = Employee.idEmployee
        JOIN
    Certificate ON Employee.idEmployee = Certificate.idEmployee
        JOIN
    Plane ON Flight.planeRegistrationNum = Plane.planeRegistrationNum
        JOIN
    PlaneModel ON Plane.modelName = PlaneModel.modelName
GROUP BY Flight.flightNum;
```


5. 

```ruby

```


6. 

```ruby

```


7. 

```ruby

```


8. 

```ruby

```


9. 

```ruby

```


10. 

```ruby

```


# Database information



