# airbnb-clone-project
## Brief Overview of the Project
The Airbnb Clone Project is a comprehensive, real-world application designed to simulate the development of a robust booking platform like Airbnb. It involves a deep dive into full-stack development, focusing on backend systems, database design, API development, and application security. 

This project enables learners to understand complex architectures, workflows, and collaborative team dynamics while building a scalable web application.

### Project Goals
1. **User Management**: Implement a secure system for user registration, authentication, and profile management.
2. **Property Management**: Develop features for property listing creation, updates, and retrieval.
3. **Booking System**: Create a booking mechanism for users to reserve properties and manage booking details.
4. **Payment Processing**: Integrate a payment system to handle transactions and record payment details.
5. **Review System**: Allow users to leave reviews and ratings for properties.
6. **Data Optimization**: Ensure efficient data retrieval and storage through database optimizations.

### Tech Stack
- **Django**
- **Django REST Framework**
- **PostgreSQL**
- **GraphQL**
- **Celery**
- **Redis**
- **Docker**
- **CI/CD Pipelines**

## Team Roles
1. **Backend Developer**: Responsible for implementing the core of the app including its algorithm and *business logic*. The backend developer is also devise the app architecture and  *database schemas* as well as the necessary integrations such as *API endpoints*. 
2. **Database Administrator**: Responsible for managing the relational *database design* as well as *indexing*, and db *optimizations*.
3. **DevOps Engineer**: Responsible for the faster deployment using *continuous integration and continuous delivery (CI/CD) Pipelines* as well as *monitoring*, and *scaling* of the backend services. 
4. **QA Engineer**: Responsible for ensuring the backend functionalities are thoroughly tested and meet quality standards as well as meeting both functional and non-functional requirements.

## Technology Stack
- **Django**: A high-level Python web framework which would be used for building the RESTful API. It would 
- **Django REST Framework**: DRF would be used for creating and managing the RESTful API endpoints. 
- **PostgreSQL**: A powerful relational database to be used to store the structured data of the project.
- **GraphQL**: GraphQL would complement the DRF because it allows for flexible and efficient querying of data. Its purpose is for efficient fetching of nested data.
- **Celery**: For handling asynchronous tasks such as sending notifications or processing payments. The role of Celery would be to offload time-consuming or periodic tasks from request-response cycle such as Auto-canceling unconfirmed bookings after timeout.
- **Redis**: Used for caching and session management.
- **Docker**: Containerization tool to ensure consistent development and deployment environments.
- **CI/CD Pipelines**: Automated pipelines for testing and deploying code changes.

## Database Design
Key entities of the database are: Users, Properties, Bookings, Reviews, and Payments.
- **Users**:
This entity stores data for all the users including the vendors and guests. 
    
    **Some important fields includes:**
    1. *user_id* - A unique identifier for each user entry. 
    2. *fullname* - The fullname of the user.
    3. *email* - The email address of the user.
    4. *is_vendor* - A boolean value that checks if the user is a vendor(landlord) or guest.
    5. *password_hash* - For security reasons, an encrypted version of the user password.

    **Relationships:**
    - *One user* can host *many properties*.
    - *One user* can make *many bookings*.
    - *One user* can leave *many reviews*.
- **Properties**:
This entity represents a listed property by a vendor-user.
    
    **Some important fields includes:**
    1. *property_id* - A unique identifier for each property entry. 
    2. *vendor_id* - A foreign key associated with the corresponding user_id of the vendor.
    3. *title* - Name/description of the listed property.
    4. *daily_price* - Amount to rent the property.
    5. *is_available* - A boolean to check if the property is available for rent.

    **Relationships:**
    - *One property* can have *many reviews*.
    - *One property* can have *many bookings*.
- **Bookings**:
This entity represents a booking made by a guest user.
    
    **Some important fields includes:**
    1. *booking_id* - A unique identifier for each booking. 
    2. *guest_id* - A foreign key associated with the corresponding user_id of the guest.
    3. *property_id* - A foreign key associated with the corresponding property_id of the property being booked.
    4. *status* - A value for the status of the booking e.g. confirmed, pending.
    5. *guests* - Number of guests allowed.

    **Relationships:**
    - *One booking* can have *one payment*.
    - *One property* can have *many bookings*.
    - *One user*(guest) can make *many bookings*.
- **Reviews**:
This entity stores data for all reviews left on the properties.
    
    **Some important fields includes:**
    1. *review_id* - A unique identifier for each review. 
    2. *property_id* - A foreign key associated with the corresponding property_id of the property being reviewed.
    3. *guest_id* - A foreign key associated with the corresponding user_id of the reviewer.
    4. *rating* - Review rating of the property e.g. 1-5 stars
    5. *comment* - Review comment. 

    **Relationships:**
    - *One property* can have *many listings*.
    - *One user* can leave *many reviews*.
- **Payments**: 
This entity stores data for details of all payment transactions on each bookings. 
    
    **Some important fields includes:**
    1. *payment_id* - A unique identifier for each payment transaction. 
    2. *booking_id* - A foreign key associated with the corresponding booking id of the booking being paid for.
    3. *amount* - Amount paid.
    4. *status* - Payment status e.g. pending, successful, failed.
    5. *transaction_date* - Payment date. 

    **Relationships:**
    - *One payment* belongs to *one booking*.