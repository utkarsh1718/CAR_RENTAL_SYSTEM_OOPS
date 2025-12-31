# Car Rental System using OOPS in C++

This repository hosts a personal project for a comprehensive Car Rental System implemented in C++.

## Project Structure

The repository is organized into the following components:

- **`DB` Folder**: This directory acts as the database, containing four CSV (Comma Separated Values) files to store persistent data.
  - `customer.csv`: Stores customer details. Columns: `UserId`, `Password`, `Name`, `CustomerRecord`, `Dues`, `NumberOfCarsRented`.
  - `employee.csv`: Stores employee details. Columns: `UserId`, `Password`, `Name`, `EmployeeRecord`, `Dues`, `NumberOfCarsRented`.
  - `manager.csv`: Stores manager credentials. Columns: `UserId`, `Password`, `Name`.
  - `car.csv`: Stores vehicle fleet information. Columns: `CarId`, `Model`, `Condition`, `RentPerDay`, `RentDate`, `DueDate`, `UserIdRented`.

- **`Model.hpp`**: This header file contains the definitions for classes, functions, and structures used throughout the system.
  - **`User` Class**: Base class for Customer, Employee, and Manager. (Attributes: UserID, Password, Name).
  - **`Customer` Class**: Inherits from User.
    - *Attributes*: CustomerRecord, Dues, NumberOfCarsRented.
    - *Functions*: Authenticate, Login, Calculate Max Rentable Cars, Return Car, Update Record, Clear Dues, Display All Customers.
  - **`Employee` Class**: Inherits from User.
    - *Attributes*: EmployeeRecord, Dues, NumberOfCarsRented.
    - *Functions*: Authenticate, Login, Calculate Max Rentable Cars, Return Car, Update Record, Clear Dues, Display All Employees.
  - **`Car` Class**:
    - *Attributes*: CarId, Model, Condition, RentPerDay, RentDate, DueDate, UserID.
    - *Functions*: Rent Car, Check Rental Status, Calculate Fines/Dues, Display Cars (Rented/Available/All).
  - **`Manager` Class**:
    - *Functions*: View all entities; Add, Update, or Modify Users and available Cars.
  - **Database Management (DBM) Classes** (`CustomerDBM`, `EmployeeDBM`, `ManagerDBM`, `CarDBM`):
    - These classes manage vectors of their respective objects to handle File I/O operations (Read/Write CSV).
    - *Capabilities*: Add, Delete, Update, Select by ID, and List all entries.
  - **`Date` Structure**: Utility structure for handling date-related operations.
  - **Utility Functions**: Date difference calculation, CSV file parsing, and numeric validation.

- **Implementation Files**:
  - `Car.cpp`: Implementation of the `Car` class.
  - `Customer.cpp`: Implementation of the `Customer` class.
  - `Employee.cpp`: Implementation of the `Employee` class.
  - `Manager.cpp`: Implementation of the `Manager` class.
  - `DB_Manager.cpp`: Implementation of the DBM classes.
  - `main.cpp`: Entry point of the application. Manages the control flow and user interaction.

## Running the Program

The system initializes with a pre-populated database containing 5 Customers, 5 Employees, 6 Cars, and 1 Manager. The default credentials and data are detailed below:

### Customers
| UserID  | Password | Name  | Customer Record |  Dues  | Number of Cars Rented |
| :-------------: | :-------------: | :-------------: | :-------------: | :-------------: | :-------------: |
| user1 | password1  | Rohan | 70 | 1000 | 0 |
| user2 | password2  | Rahul | 80 | 1250 | 1 |
| user3 | password3  | Karan | 90 | 2000 | 0 |
| user4 | password4  | Amogh | 85 | 3000 | 0 |
| user5 | password5  | Rajat | 95 | 1400 | 2 |

### Employees
| UserID  | Password | Name  | Employee Record |  Dues  | Number of Cars Rented |
| :-------------: | :-------------: | :-------------: | :-------------: | :-------------: | :-------------: |
| employee1 | password1  | Ben | 65 | 1300 | 1 |
| employee2 | password2  | Tom | 95 | 1800 | 0 |
| employee3 | password3  | Hog | 40 | 2200 | 0 |
| employee4 | password4  | Adi | 65 | 2600 | 1 |
| employee5 | password5  | Jen | 70 | 9800 | 0 |

### Manager
| UserID  | Password | Name  |
| :-------------: | :-------------: | :-------------: |
| manager1 | password1  | Harry |

### Cars
| CarID  | Model | Condition  | Rent per Day (Rs.) |  Rent Date  | Due Date | UserID of who rented |
| :-------------: | :-------------: | :-------------: | :-------------: | :-------------: | :-----------: | :-----------: |
| UP1818 | Tata | 8 | 2000 | 27-02-2024 | 04-03-2024 | user2 |
| UK1812 | Mahindra | 9 | 2500 |  |  |  |
| MH3632 | Toyota | 6 | 2200 | 28-02-2024 | 07-03-2024 | user5 |
| DL9891 | Hyundai | 7 | 2000 | 24-02-2024 | 01-03-2024 | user5 |
| GJ5172 | Maruti | 5 | 1800 | 15-02-2024 | 03-03-2024 | employee1 |
| UP8728 | Skoda | 8 | 3000 | 23-02-2024 | 08-03-2024 | employee4 |

**NOTE:** In the Cars database, if a vehicle is not currently rented, the `Due Date`, `Rent Date`, and `UserID of who rented` fields are left blank.

## Assumptions and Design Logic

- **Data Integrity:** A Car currently rented by a User cannot be deleted or updated by the Manager.
- **User Deletion:** If a Manager deletes a User, any cars currently rented by that User are automatically processed as returned.
- **Car Condition:** Rated on a scale of `0 to 10` (0 = very bad, 10 = excellent).
- **User Records:** Both Customers and Employees have a "reliability record" on a scale of `0 to 100` (0 = bad, 100 = good).
- **New Users:** If the database is empty or a new User is added, they are assigned a default record score of `80`.
- **Rental Limit:** A User can rent a maximum of `(User Record)/30 + 1` cars at a time.
- **Dynamic Updates:** When a car is returned, its condition may improve or worsen. The User's record is updated algorithmically based on the change in car condition and adherence to the due date.
- **Rental Duration:** The maximum rental period allowed is 200 days.
- **Input Constraints:** Attributes like `UserID`, `CarID`, `Name`, `Model`, and `Password` are treated as single words. If multi-word input is provided, only the first word is processed.

## Portability

The code was developed on the **Windows** operating system.

## Author
- **Utkarsh Singh**
- Electrical Engineering
- IIT Kanpur
- 241117
