# simple-job-app
Simple Job App
---

## **SimpleJobApp: Microservices Job Posting Platform**

### **Overview**

**SimpleJobApp** is a microservices-based platform designed for posting and viewing job listings. The application consists of two services:

1. **Job Service**: Allows users to create and post new job listings.
2. **Job Listing Service**: Retrieves and displays the list of jobs from the database.

The system is built using Node.js and Express for the services, with MySQL used as the central database.

### **Project Structure**

```bash
SimpleJobApp/
│
├── job-service/           # Service to add job listings
│   ├── src/
│   │   ├── index.js       # Main entry point for job service
│   │   ├── routes/
│   │   │   └── job.js     # Route handling job creation
│   │   └── db.js          # Database connection setup
│   └── Dockerfile         # Dockerfile for job service
│
├── job-listing-service/   # Service to display job listings
│   ├── src/
│   │   ├── index.js       # Main entry point for listing service
│   │   ├── routes/
│   │   │   └── jobs.js    # Route handling job retrieval
│   │   └── db.js          # Database connection setup
│   └── Dockerfile         # Dockerfile for job listing service
│
├── db/                    # MySQL database configuration
│   ├── schema.sql         # SQL script to create database and jobs table
│   └── Dockerfile         # Dockerfile for MySQL setup
│
├── docker-compose.yml      # Docker Compose file to run all services together
└── README.md               # Project documentation
```

### **Services Overview**

1. **Job Service**:
   - **Function**: Handles creating and adding new job listings.
   - **Endpoint**:
     - `POST /job`: Adds a new job listing.
   - **Port**: 3001
   - **Tech Stack**: Node.js, Express, MySQL

2. **Job Listing Service**:
   - **Function**: Retrieves and displays all job listings from the database.
   - **Endpoint**:
     - `GET /jobs`: Retrieves the list of jobs.
   - **Port**: 3002
   - **Tech Stack**: Node.js, Express, MySQL

3. **Database**:
   - **Function**: Stores job data such as title, description, location, and salary.
   - **Database**: MySQL
   - **Port**: 3306

### **How to Set Up and Run the Project**

#### **Prerequisites**:
Make sure you have the following installed:
- **Docker**: To containerize and run the services.
- **Docker Compose**: To orchestrate the services.

#### **Steps to Run the Application**:

1. **Clone the repository**:
   ```bash
   git clone https://github.com/yourusername/SimpleJobApp.git
   cd SimpleJobApp
   ```

2. **Build and start all services using Docker Compose**:
   ```bash
   docker-compose up --build
   ```

   This command will:
   - Set up the **Job Service** on port 3001.
   - Set up the **Job Listing Service** on port 3002.
   - Initialize the **MySQL Database** on port 3306.

3. **Access the Services**:

   - **Job Service** (Add jobs): `POST` requests can be sent to `http://localhost:3001/job`.
   - **Job Listing Service** (View jobs): `GET` requests can be sent to `http://localhost:3002/jobs`.

### **Usage Example**

#### 1. **Adding a Job Listing** (via Job Service):
```bash
POST http://localhost:3001/job
Content-Type: application/json

{
  "title": "Electrician",
  "description": "Looking for an experienced electrician.",
  "location": "Mumbai",
  "salary": 500.00
}
```

#### 2. **Viewing Job Listings** (via Job Listing Service):
```bash
GET http://localhost:3002/jobs
```

**Example Response**:
```json
[
  {
    "id": 1,
    "title": "Electrician",
    "description": "Looking for an experienced electrician.",
    "location": "Mumbai",
    "salary": 500.00
  }
]
```

### **Database Schema**

The MySQL database contains one table: `jobs`.

```sql
CREATE DATABASE IF NOT EXISTS jobDB;

USE jobDB;

CREATE TABLE IF NOT EXISTS jobs (
  id INT AUTO_INCREMENT PRIMARY KEY,
  title VARCHAR(255) NOT NULL,
  description TEXT,
  location VARCHAR(255),
  salary DECIMAL(10, 2)
);
```

### **Docker Setup**

- The **Job Service** and **Job Listing Service** are containerized with Node.js.
- The **Database** service is containerized with MySQL 5.7.
- Docker Compose orchestrates the services.

To rebuild and restart the services:
```bash
docker-compose down
docker-compose up --build
```

### **Contributing**

Feel free to open issues or submit pull requests if you have suggestions for improving the platform.

### **License**

This project is licensed under the MIT License.

---

This **README** provides an overview of the project, its structure, and instructions for setup and usage. Let me know if you need any further modifications!
