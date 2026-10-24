# ER Diagram Workshop – Submission Template

## Objective
To understand and apply ER modeling concepts by creating ER diagrams for real-world applications.

## Purpose
Gain hands-on experience in designing ER diagrams that represent database structure including entities, relationships, attributes, and constraints.

---

# Scenario A: City Fitness Club Management

**Business Context:**  
FlexiFit Gym wants a database to manage its members, trainers, and fitness programs.

**Requirements:**  
- Members register with name, membership type, and start date.  
- Each member can join multiple programs (Yoga, Zumba, Weight Training).  
- Trainers assigned to programs; a program may have multiple trainers.  
- Members may book personal training sessions with trainers.  
- Attendance recorded for each session.  
- Payments tracked for memberships and sessions.

### ER Diagram:
*Paste or attach your diagram here*  
<img width="397" height="626" alt="image" src="https://github.com/user-attachments/assets/7f27c8bb-6aa1-4060-bbd8-99d64ad0e863" />
<img width="982" height="667" alt="City fitness club drawio" src="https://github.com/user-attachments/assets/e9248545-715a-416d-b0ff-625b0d087595" />


### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
| Member       |  M_ID (PK), Name, Type, Start_date, Email_ID, Phone                  | Stores member details      |
| Membership       | M_ID (PK, FK), Type, Start_date, End_date, Fee                    | Membership details linked to Member      |
| Program       |   P_ID (PK), Name, Description, Duration                 | Fitness programs such as Yoga, Zumba, Weight Training      |
| Trainer       | T_ID (PK), Name, Designation, Phone                   | Trainer details      |
| Session       | S_ID (PK), Date, Time, Status                   | Personal training session details      |
| Payment       | P_ID (PK), Amount, Payment_date, Status                   | Payment details      |
| Attendance       | A_ID (PK), Date, Status                   | Records session attendance      |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
| Member — Enrolls — Program             | M:N           | Partial on both sides              | Members can enroll in multiple programs, and programs can have multiple members      |
| Member — Holds — Membership             | 1:N           | Membership: Total participation; Member: Partial participation              | A member can hold membership records over time       |
| Membership — Makes — Payment |	1:N	| Payment: Total participation ; Membership: Partial participation	| Membership payments are recorded
| Payment — For — Session |	N:1	| Payment: Total participation ; Session: Partial participation |	A payment is for a training session |
| Trainer — Conducts — Session |	1:N	| Session: Total participation ; Trainer: Partial participation |	A trainer can conduct multiple sessions |
| Session — Records — Attendance |	1:1 |	Total on both sides |	Each session has an attendance record |
| Program — Handled by — Trainer |	M:N	| Partial on both sides |	A program can have multiple trainers, and trainers can handle multiple programs |          

### Assumptions
- Each member has a unique M_ID.
- Each program has a unique P_ID, and each trainer has a unique T_ID.
- A member can enroll in multiple programs, and each program can have multiple members.
- A member can hold membership records over time.
- Membership payments are linked to Membership, while session payments are linked to Session.
- Each session is conducted by a trainer and has an attendance record.
- The diagram uses P_ID for both Program and Payment. In an implemented database, use distinct primary keys such as Program_ID and Payment_ID to avoid ambiguity.

---

# Scenario B: City Library Event & Book Lending System

**Business Context:**  
The Central Library wants to manage book lending and cultural events.

**Requirements:**  
- Members borrow books, with loan and return dates tracked.  
- Each book has title, author, and category.  
- Library organizes events; members can register.  
- Each event has one or more speakers/authors.  
- Rooms are booked for events and study.  
- Overdue fines apply for late returns.

### ER Diagram:
*Paste or attach your diagram here*  
<img width="362" height="578" alt="image" src="https://github.com/user-attachments/assets/26a7392f-5bd2-4817-b0e3-04337a1d9beb" />
<img width="1462" height="692" alt="library management drawio" src="https://github.com/user-attachments/assets/2ae5ddd0-51a5-4a1d-a51c-6a0fdf666969" />


### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
| Member |	M_ID (PK), Name, Phone, Email, Join_date |	Stores member details |
| BOOK_LOAN |	L_ID (PK), Loan_date, Return_date, Status, M_ID (FK), B_ID (FK) |	Records book borrowing transactions |
| BOOK |	B_ID (PK), Title, Author, ISBN, Category |	Stores book details |
| Speaker |	S_ID (PK), Name, Bio, Email, Contact, Phone	| Stores speaker/author details |
| Event_speaker |	E_ID (FK), S_ID (FK), Designation	| Connects events with speakers |
| Event |	E_ID (PK), Title, Description, Date, Time	| Stores library event details |
| FINE |	Fine_ID (PK), L_ID (FK), Amount, Date, Reason |	Records overdue book fines |
| ROOM |	R_ID (PK), Name, Type, Capacity	| Stores room details       |                 

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
| Member — borrows — BOOK_LOAN |	1:N |	BOOK_LOAN: Total participation; Member: Partial participation |	A member can borrow multiple books |
| BOOK_LOAN — for — BOOK |	N:1	| BOOK_LOAN: Total participation; BOOK: Partial participation |	Each loan refers to one book |
| Member — registers — Event |	M:N	| Partial on both sides |	Members can register for multiple events |
| Speaker — speaks — Event_speaker |	1:N	| Event_speaker: Total participation; Speaker: Partial participation |	A speaker can participate in multiple events |
| Event_speaker — has — Event |	N:1	| Event_speaker: Total participation; Event: Total participation |	Each event-speaker record links one speaker to one event |
| BOOK_LOAN — generates — FINE |	1:0..1 | FINE: Total; BOOK_LOAN: Partial |	A loan may generate a fine for late return |
| Member — pays — FINE |	1:N	| FINE: Total participation; Member: Partial participation |	A member can pay multiple fines |
| Event — held in — ROOM |	N:1	| Event: Total; ROOM: Partial |	Each event takes place in one room             |         

### Assumptions
- Each member, book, loan, event, speaker, room, and fine has a unique identifier.
- A member can borrow multiple books, and each loan refers to one member and one book.
- A fine is generated only when a loan incurs an overdue charge; a loan may have no fine.
- Members can register for multiple events, and each event can have multiple registered members.
- An event can have multiple speakers, and a speaker can participate in multiple events.
- Each event is assigned to one room, while a room can host different events at different times.
- Room bookings for individual study purposes are not explicitly represented in this diagram; a separate ROOM_BOOKING entity would be needed to manage them.

---

# Scenario C: Restaurant Table Reservation & Ordering

**Business Context:**  
A popular restaurant wants to manage reservations, orders, and billing.

**Requirements:**  
- Customers can reserve tables or walk in.  
- Each reservation includes date, time, and number of guests.  
- Customers place food orders linked to reservations.  
- Each order contains multiple dishes; dishes belong to categories (starter, main, dessert).  
- Bills generated per reservation, including food and service charges.  
- Waiters assigned to serve reservations.

### ER Diagram:
*Paste or attach your diagram here*  
<img width="395" height="587" alt="image" src="https://github.com/user-attachments/assets/1bff3769-6925-4e20-8d42-9894036a63b9" />
<img width="942" height="722" alt="Restaurant management drawio" src="https://github.com/user-attachments/assets/ed1631ac-b45e-472a-933d-bc88c72e4331" />


### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
| Customer |	C_ID (PK), Name, Address (City, St_Name, Pin), Phone, Email	| Stores customer details; Phone and Email are multivalued attributes in the diagram |
| Reservation |	Reservation_ID (PK), Date, Time, No_of_Guests, Type, C_ID (FK), W_ID (FK) |	Stores reservation details, including advance bookings and walk-ins |
| Waiter |	W_ID (PK), Name, Phone, Shift |	Stores waiter details |
| ORDER	| Order_ID (PK), Date, Status, Total_Amount, Reservation_ID (FK) |	Stores food orders linked to reservations |
| BILL |	Bill_ID (PK), Total_Amount, Bill_Date, Payment_Status, Service_Charge, Tax, Reservation_ID (FK)	| Stores billing details for reservations |
| ORDER_ITEM | Item_ID (PK), Order_ID (FK), Dish_ID (FK), Quantity, Price |	Records individual dishes and their quantities in an order |
| DISH |	Dish_ID (PK), Name, Price, Description, Category_ID (FK)| Stores food item details |
| CATEGORY |	Category_ID (PK), Name | Stores dish categories, such as starters, main course, and desserts       |                   

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
| Customer — makes — Reservation |	1:N	| Reservation: Total; Customer: Partial	| A customer can make multiple reservations |
| Reservation — assigned_to — Waiter |	N:1	| Reservation: Total; Waiter: Partial |	Each reservation is assigned to one waiter |
| Reservation — places — Order |	1:N	| Order: Total; Reservation: Partial	| A reservation can have multiple orders |
| Reservation — generates — Bill |	1:1 |	Bill: Total; Reservation: Partial	| Each bill belongs to one reservation; a reservation may not yet have a bill |
| Order — contains — Order_Item |	1:N	| Order_Item: Total; Order: Total |	Each order contains one or more order items |
| Order_Item — refers_to — Dish |	N:1	| Order_Item: Total; Dish: Partial |Each order item refers to one dish |
| Dish — belongs_to — Category |	N:1	| Dish: Total; Category: Partial  | Each dish belongs to one category             |         

### Assumptions
- Each customer has a unique C_ID, and each waiter has a unique W_ID.
- A customer can make multiple reservations, and reservations can be made in advance or as walk-ins.
- Each reservation records its date, time, number of guests, and reservation type.
- Each reservation is assigned to one waiter, and a waiter can serve multiple reservations.
- Each order is associated with a reservation and can contain multiple dishes through ORDER_ITEM.
- A dish belongs to one category, such as starter, main course, or dessert.
- A bill is generated for a reservation and includes the food total, service charge, and tax.
- Phone and Email are multivalued attributes in the reference diagram. In a relational database, these can be stored in separate tables if customers may have multiple phone numbers or email addresses.
 
---

## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**
