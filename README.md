# MIST4610-Group-Project-1-StudentDorms
Team Name

59925 Group 3

Team Members: <br>
David Kenny @djk42296 <br>
Sahasra Manchikanti @sahasra-22 <br>
Grant Harris <br>
Joseph Enck <br>
Sofia Drescher <br>

Problem Description: <br>
The task at hand is to design and develop a relational database for the overall operations of a university housing system. The primary entity in the model is the Residence Hall entity of the housing system, with each Residence Hall representing an individual dormitory facility that the university owns and maintains across campus. The Residence Hall functions alongside dorm floors, student rooms, resident assistants, maintenance requests, and parking assignments that serve the students living within university housing. We aim to accurately represent these relationships, create sample data, and populate the entities and their corresponding attributes with this information. In addition, we intend to perform functional queries on the data so that they may provide meaningful insight into the housing system and its day-to-day operations.

Data Model: <br>
  The data model represents the core operations of a university housing management system. It is designed to store information about residence halls, dorm floors, rooms, students, resident assistants (RAs), university housing staff, maintenance requests, inspections, and parking assignments. Each of these entities interacts in ways that reflect how a real university housing system functions on a daily basis. <br>
  The Residence Hall entity serves as the foundation of the model, with each hall containing multiple Dorm Floors, and each floor consisting of several Rooms. The Students entity stores personal information about each student living on campus, such as their name, phone number, class year, and assigned RA. Each student is connected to a specific room through the DormAssignments table, allowing the database to track which student resides in which room. <br>
  Each Resident Assistant is also linked to both a Dorm Floor and a Student record, representing that RAs are students themselves who oversee a particular floor. The Inspections entity stores information about room inspections conducted by RAs, including the inspection score and the room being inspected. <br>
  The model also includes MaintenanceRequests, which connect rooms to UGAStaff members responsible for resolving maintenance issues. This allows the system to record who submitted the request, which room it pertains to, and which staff member completed the work. Finally, the Parking entity tracks parking locations and associates them with students who have been assigned parking spaces. <br>
  Overall, the database supports storage of all key data related to housing logistics, such as student assignments, staff information, maintenance activity, and inspection records. However, it does not store financial data such as rent payments or billing, nor does it include academic information like student grades or course enrollment. The model focuses strictly on operational and residential management within university housing. <br>


<img width="1041" height="584" alt="MIST 4610 Project 1 Data Model" src="https://github.com/user-attachments/assets/44f5ebf1-4877-4ef4-88e6-f19bc57d6e14" />

Data Dictionary:

<img width="659" height="271" alt="Screenshot 2025-10-26 at 3 52 04 PM" src="https://github.com/user-attachments/assets/5ee9afce-da50-4589-9406-426ef031b51f" />
<img width="659" height="387" alt="Screenshot 2025-10-26 at 3 52 23 PM" src="https://github.com/user-attachments/assets/a0b6425a-7337-453f-a17d-953fcf5ca8f2" />
<img width="655" height="450" alt="Screenshot 2025-10-26 at 3 52 48 PM" src="https://github.com/user-attachments/assets/d2c08db7-c0b2-4aa4-9cfb-8ab58c96deaf" />
<img width="652" height="368" alt="Screenshot 2025-10-26 at 3 53 14 PM" src="https://github.com/user-attachments/assets/fb71d065-20e5-4eb2-bc48-d343719b7e57" />
<img width="655" height="390" alt="Screenshot 2025-10-26 at 3 53 39 PM" src="https://github.com/user-attachments/assets/f343ae80-b315-4ea3-9358-9d32eeb98738" />
<img width="657" height="258" alt="Screenshot 2025-10-26 at 3 53 53 PM" src="https://github.com/user-attachments/assets/250b58ea-9ef9-4876-bff4-91d29390e8ef" />
<img width="648" height="435" alt="Screenshot 2025-10-26 at 3 54 17 PM" src="https://github.com/user-attachments/assets/aad41437-9dde-4217-a4cb-193f3a05f3c8" />
<img width="660" height="539" alt="Screenshot 2025-10-26 at 3 55 02 PM" src="https://github.com/user-attachments/assets/8e346adc-5fe5-4bb3-a58c-5bb44ffe586e" />
<img width="662" height="353" alt="Screenshot 2025-10-26 at 3 55 23 PM" src="https://github.com/user-attachments/assets/fc556c64-2b71-4bdf-a02b-2c29cc0eb4e9" />












