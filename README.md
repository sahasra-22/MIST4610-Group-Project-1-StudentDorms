# MIST4610-Group-Project-1-StudentDorms

# **MIST 4610 Group Project 1 Team 3**
**Team Name** <br>
59925 Group 3

## **Team Members:** <br>
David Kenny @djk42296 <br>
Sahasra Manchikanti @sahasra-22 <br>
Grant Harris <br>
Joseph Enck <br>
Sofia Drescher <br>

## **Problem Description:** <br>
The task at hand is to design and develop a relational database for the overall operations of a university housing system. The primary entity in the model is the Residence Hall entity of the housing system, with each Residence Hall representing an individual dormitory facility that the university owns and maintains across campus. The Residence Hall functions alongside dorm floors, student rooms, resident assistants, maintenance requests, and parking assignments that serve the students living within university housing. We aim to accurately represent these relationships, create sample data, and populate the entities and their corresponding attributes with this information. In addition, we intend to perform functional queries on the data so that they may provide meaningful insight into the housing system and its day-to-day operations.

## **Data Model:** <br>
  The data model represents the core operations of a university housing management system. It is designed to store information about residence halls, dorm floors, rooms, students, resident assistants (RAs), university housing staff, maintenance requests, inspections, and parking assignments. Each of these entities interacts in ways that reflect how a real university housing system functions on a daily basis. <br>
  The Residence Hall entity serves as the foundation of the model, with each hall containing multiple Dorm Floors, and each floor consisting of several Rooms. The Students entity stores personal information about each student living on campus, such as their name, phone number, class year, and assigned RA. Each student is connected to a specific room through the DormAssignments table, allowing the database to track which student resides in which room. <br>
  Each Resident Assistant is also linked to both a Dorm Floor and a Student record, representing that RAs are students themselves who oversee a particular floor. The Inspections entity stores information about room inspections conducted by RAs, including the inspection score and the room being inspected. <br>
  The model also includes MaintenanceRequests, which connect rooms to UGAStaff members responsible for resolving maintenance issues. This allows the system to record who submitted the request, which room it pertains to, and which staff member completed the work. Finally, the Parking entity tracks parking locations and associates them with students who have been assigned parking spaces. <br>
  Overall, the database supports storage of all key data related to housing logistics, such as student assignments, staff information, maintenance activity, and inspection records. However, it does not store financial data such as rent payments or billing, nor does it include academic information like student grades or course enrollment. The model focuses strictly on operational and residential management within university housing. <br>


<img width="1041" height="584" alt="MIST 4610 Project 1 Data Model" src="https://github.com/user-attachments/assets/44f5ebf1-4877-4ef4-88e6-f19bc57d6e14" />

## **Data Dictionary:**

<img width="659" height="271" alt="Screenshot 2025-10-26 at 3 52 04 PM" src="https://github.com/user-attachments/assets/5ee9afce-da50-4589-9406-426ef031b51f" />
<img width="659" height="387" alt="Screenshot 2025-10-26 at 3 52 23 PM" src="https://github.com/user-attachments/assets/a0b6425a-7337-453f-a17d-953fcf5ca8f2" />
<img width="655" height="450" alt="Screenshot 2025-10-26 at 3 52 48 PM" src="https://github.com/user-attachments/assets/d2c08db7-c0b2-4aa4-9cfb-8ab58c96deaf" />
<img width="652" height="368" alt="Screenshot 2025-10-26 at 3 53 14 PM" src="https://github.com/user-attachments/assets/fb71d065-20e5-4eb2-bc48-d343719b7e57" />
<img width="655" height="390" alt="Screenshot 2025-10-26 at 3 53 39 PM" src="https://github.com/user-attachments/assets/f343ae80-b315-4ea3-9358-9d32eeb98738" />
<img width="657" height="258" alt="Screenshot 2025-10-26 at 3 53 53 PM" src="https://github.com/user-attachments/assets/250b58ea-9ef9-4876-bff4-91d29390e8ef" />
<img width="648" height="435" alt="Screenshot 2025-10-26 at 3 54 17 PM" src="https://github.com/user-attachments/assets/aad41437-9dde-4217-a4cb-193f3a05f3c8" />
<img width="660" height="539" alt="Screenshot 2025-10-26 at 3 55 02 PM" src="https://github.com/user-attachments/assets/8e346adc-5fe5-4bb3-a58c-5bb44ffe586e" />
<img width="662" height="353" alt="Screenshot 2025-10-26 at 3 55 23 PM" src="https://github.com/user-attachments/assets/fc556c64-2b71-4bdf-a02b-2c29cc0eb4e9" />


## **Queries:** <br>
<img width="680" height="478" alt="Screenshot 2025-10-26 at 3 58 39 PM" src="https://github.com/user-attachments/assets/988d3293-01a6-4e03-934b-3d96f033603e" />

### **QUERY 1 - ResidenceHallRequests** <br>
SELECT ResidenceHall.address, COUNT(MaintainanceRequests.requestID) AS NumberOfRequests <br>
FROM MaintainanceRequests <br>
JOIN Rooms ON MaintainanceRequests.roomID = Rooms.roomID <br>
JOIN DormFloor ON Rooms.DormFloor_floorID = DormFloor.floorID <br>
JOIN ResidenceHall ON DormFloor.residenceHallID = ResidenceHall.residenceHallID <br>
GROUP BY ResidenceHall.address <br>
HAVING COUNT(MaintainanceRequests.requestID) > 1; <br>

<img width="651" height="114" alt="Screenshot 2025-10-26 at 4 08 34 PM" src="https://github.com/user-attachments/assets/257dfdef-d5ef-4186-b343-3367637662ee" />

Query 1 allows managers to see which residence halls have had the most maintenance requests. This helps managers identify which buildings may be experiencing more issues and therefore require more frequent maintenance checks, additional staff, or updated facilities. By listing only halls with more than one request, the query filters out isolated incidents and focuses on areas with recurring problems that may need further investigation. 

### **QUERY 2 - InspectionStats()** <br>
SELECT ResidenceHall.address, COUNT(Inspections.inspectionID) AS TotalInspections, <br>
(SELECT COUNT(*) FROM Inspections JOIN Rooms ON Inspections.roomID = Rooms.roomID <br>
JOIN DormFloor ON Rooms.DormFloor_floorID = DormFloor.floorID  <br>
WHERE DormFloor.residenceHallID = ResidenceHall.residenceHallID <br>
AND Inspections.inspectionScore = 'Pass') AS TotalPasses <br>
FROM Inspections <br>
JOIN Rooms ON Inspections.roomID = Rooms.roomID <br>
JOIN DormFloor ON Rooms.DormFloor_floorID = DormFloor.floorID <br>
JOIN ResidenceHall ON DormFloor.residenceHallID = ResidenceHall.residenceHallID <br>
GROUP BY ResidenceHall.address, ResidenceHall.residenceHallID <br>
ORDER BY TotalPasses DESC; <br>

<img width="631" height="142" alt="Screenshot 2025-10-26 at 4 08 48 PM" src="https://github.com/user-attachments/assets/d7ed720a-6e5f-474f-9849-bec861810f70" />

Query 2 allows managers to see how many inspections each residence hall has had, along with how many of those inspections passed. This helps managers identify which buildings are performing well during inspections and which may require improvements. Ordering the results by the number of passes allows managers to quickly identify the most compliant residence halls and prioritize those that need additional attention or maintenance.

### **QUERY 3 - StudentParking** <br>
SELECT ResidenceHall.address, COUNT(Students.studentID) AS TotalStudents, <br>
(COUNT(Students.studentID)-(SELECT COUNT(Parking.studentID) FROM Parking <br>
JOIN Students ON Parking.studentID = Students.studentID <br>
JOIN DormFloor ON Students.floorID = DormFloor.floorID <br>
WHERE DormFloor.residenceHallID = ResidenceHall.residenceHallID)) AS StudentsWithoutParking <br>
FROM ResidenceHall <br>
JOIN DormFloor ON ResidenceHall.residenceHallID = DormFloor.residenceHallID <br>
JOIN Students ON Students.floorID = DormFloor.floorID <br>
GROUP BY ResidenceHall.residenceHallID, ResidenceHall.address <br>
ORDER BY StudentsWithoutParking DESC; <br>

<img width="626" height="173" alt="Screenshot 2025-10-26 at 4 09 03 PM" src="https://github.com/user-attachments/assets/7fc2baa6-95cf-40a3-a03b-2f0efe698bfc" />

Query 3 allows managers to compare the total number of students in each residence hall to the number of those students who have parking spaces. This provides insight into how many students live in each hall without access to parking, which can help determine if additional parking spaces are needed. If a hall shows a large number of students without parking, it may indicate a need to expand parking options or provide alternative transportation services.

### **QUERY 4 - RAAssignments** <br>
WITH ra_boss AS (SELECT DISTINCT studentID, studentName FROM Students <br>
WHERE studentID IN (SELECT DISTINCT raID FROM Students)), ra_worker AS (SELECT * FROM Students) <br>
SELECT ra_boss.studentName AS "RA", ra_worker.studentName AS "Student" <br>
FROM ra_boss JOIN ra_worker ON ra_worker.raID = ra_boss.studentID <br>
ORDER BY ra_boss.studentName, ra_worker.studentName; <br>

<img width="564" height="246" alt="Screenshot 2025-10-26 at 4 09 15 PM" src="https://github.com/user-attachments/assets/bc04c67f-2527-4759-bbce-5fb9dab0abc8" />

Query 4 allows managers to see which students are Resident Assistants (RAs) and which students are under their supervision. This helps managers visualize the hierarchical structure of RAs and their assigned residents, ensuring that each student is appropriately paired with an RA. Organizing the results by RA name makes it easier to see who manages which students and confirm that all residents are accounted for.

### **QUERY 5 - StudentMaintenanceRequests** <br>
SELECT Students.studentName, Rooms.roomID, MaintainanceRequests.requestID FROM Students <br>
JOIN DormFloor ON Students.floorID = DormFloor.floorID <br>
JOIN Rooms ON DormFloor.floorID = Rooms.DormFloor_floorID <br>
JOIN MaintainanceRequests ON Rooms.roomID = MaintainanceRequests.roomID <br>
ORDER BY Students.studentName, MaintainanceRequests.requestID; <br>

<img width="585" height="230" alt="Screenshot 2025-10-26 at 4 09 26 PM" src="https://github.com/user-attachments/assets/d3120550-a648-4f9a-b0b8-ef676b1c4368" />

Query 5 allows managers to identify which students have maintenance requests connected to their rooms. This can be used to track which rooms are experiencing issues and which students are affected. By listing students alongside their room IDs and maintenance request IDs, managers can easily follow up with the responsible staff and ensure that requests are resolved promptly.

### **QUERY 6 - StaffRequests** <br>
SELECT UGAstaff.staffName, ResidenceHall.address, COUNT(MaintainanceRequests.requestID) AS NumRequests FROM MaintainanceRequests <br>
JOIN UGAstaff ON MaintainanceRequests.staffID = UGAstaff.staffID <br>
JOIN Rooms ON MaintainanceRequests.roomID = Rooms.roomID <br>
JOIN DormFloor ON Rooms.DormFloor_floorID = DormFloor.floorID <br>
JOIN ResidenceHall ON DormFloor.residenceHallID = ResidenceHall.residenceHallID <br>
GROUP BY UGAstaff.staffName, ResidenceHall.address <br>
ORDER BY UGAstaff.staffName, ResidenceHall.address; <br>

<img width="553" height="235" alt="Screenshot 2025-10-26 at 4 09 39 PM" src="https://github.com/user-attachments/assets/123f8f6a-dd24-4acd-ae06-d5f41da0b7da" />

Query 6 allows managers to see which staff members have handled the most maintenance requests in each residence hall. This helps identify which staff are most active or which buildings require the most staff attention. Managers can use this information to evaluate workload distribution, recognize high-performing employees, and ensure that maintenance staff are allocated effectively across all halls.

### **QUERY 7 - GetAllRequests** <br>
SELECT MaintainanceRequests.requestID, MaintainanceRequests.roomID, UGAstaff.staffName, UGAstaff.staffPhone <br>
FROM MaintainanceRequests <br>
JOIN UGAstaff ON MaintainanceRequests.staffID = UGAstaff.staffID; <br>

<img width="660" height="234" alt="Screenshot 2025-10-26 at 4 10 00 PM" src="https://github.com/user-attachments/assets/f65637e5-d07e-4b7c-9061-4e35ed8dd8cf" />

Query 7 allows managers to view all maintenance requests along with the staff member responsible for each one. This provides an easy way to match staff names and contact information to specific requests, allowing managers to follow up on progress or assign new tasks efficiently.

### **QUERY 8 - StudentsWithParking** <br>
SELECT studentName, <br>
(SELECT lotLocation FROM Parking  <br>
WHERE Parking.studentID = Students.studentID) AS lotLocation <br>
FROM Students <br>
WHERE EXISTS (SELECT 1 FROM Parking <br>
WHERE Parking.studentID = Students.studentID);

<img width="555" height="212" alt="Screenshot 2025-10-26 at 4 10 27 PM" src="https://github.com/user-attachments/assets/93d8f3b6-b352-4a92-a6da-adb9868fd50f" />

Query 8 allows managers to see which students have parking spaces and where those spaces are located. This can help the management team confirm that parking assignments are accurate and up to date. It also ensures that only students who actually have parking spots appear in the results, simplifying record verification.

### **QUERY 9 - RoomLocations** <br>
SELECT Rooms.roomID, DormFloor.floorNumber, ResidenceHall.address <br>
FROM Rooms <br>
JOIN DormFloor ON Rooms.DormFloor_floorID = DormFloor.floorID <br>
JOIN ResidenceHall ON DormFloor.residenceHallID = ResidenceHall.residenceHallID; 

<img width="642" height="237" alt="Screenshot 2025-10-26 at 4 10 41 PM" src="https://github.com/user-attachments/assets/00d2c48c-2a09-4d2a-b9d6-7b921b8c0f75" />

Query 9 allows managers to view which rooms belong to which floors and which residence halls. This provides a clear understanding of the building layout and structure. It helps management easily identify where each room is located, which is useful for maintenance, inspections, or housing assignments.

### **QUERY 10 - StudentRooms** <br>
SELECT Students.studentName, Rooms.roomID FROM Students <br>
JOIN DormFloor ON Students.floorID = DormFloor.floorID <br>
JOIN Rooms ON DormFloor.floorID = Rooms.DormFloor_floorID;

<img width="627" height="208" alt="Screenshot 2025-10-26 at 4 10 59 PM" src="https://github.com/user-attachments/assets/7247aa71-26ca-4d01-be8c-c3ec3a187c7a" />

Query 10 allows managers to see which room each student is associated with. This helps confirm that every student is correctly assigned to a room and provides an organized way to verify housing records. It also allows managers to identify which floors and rooms are occupied, assisting with housing capacity planning.












