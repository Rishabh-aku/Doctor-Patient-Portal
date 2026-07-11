# 🏥 Doctor-Patient Portal (Advanced Java Web Application)

Welcome to the **Doctor-Patient Portal**, an advanced Java-based enterprise web application designed to streamline interactions between patients, doctors, and administrators. The application allows users to register, book doctor appointments, view appointment history, and receive prescriptions, while providing doctors and admins with dedicated portals to manage specialist, doctor details, and patient feedback.

---

## 🛠️ Technology Stack

This application is built using standard Java Web technologies:

-   **Backend Core:** Advanced Java (Servlets, JDBC)
-   **Templating & View:** JavaServer Pages (JSP), JSTL (JSP Standard Tag Library)
-   **Frontend Styling:** HTML5, CSS3, Bootstrap 5, Font Awesome (Icons)
-   **Database:** MySQL (Connector J 8.0.28)
-   **Build Management:** Apache Maven

---

## 🚀 Key Features

### 👤 Patient (User) Module
-   **Self Registration & Secure Login:** Register and access dashboard.
-   **Book Appointments:** Choose appointment date, specify illness, select specialist/doctor, and submit.
-   **View Appointment History:** Track status of appointments (Pending, or completed with doctor's prescription/comments).
-   **Profile Security:** Change accounts credentials securely.

### 🥼 Doctor Module
-   **Dedicated Login:** Access personal doctor dashboard.
-   **Appointment Tracker:** View all scheduled appointments assigned to them.
-   **Prescribe/Comment:** Provide treatment feedback and prescribe medicine to patient.
-   **Profile Settings:** Edit profile info and update security credentials.

### 🔑 Administrator Module
-   **Central Admin Dashboard:** Comprehensive stats (Total Doctors, Patients, Appointments, and Specialists).
-   **Specialist Management:** Add new medical departments/specialists.
-   **Doctor Directory:** Register new doctors, edit credentials, or remove doctors.
-   **Patient Appointment View:** Real-time monitoring of all hospital-wide appointments.

---

## 🗄️ Database Setup & Schema

To run this application locally, you will need to set up a MySQL database. Follow the SQL script below to create the database and tables:

```sql
-- 1. Create the database
CREATE DATABASE IF NOT EXISTS hospital;
USE hospital;

-- 2. Create User Details Table
CREATE TABLE `user_details` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `full_name` VARCHAR(255) NOT NULL,
  `email` VARCHAR(255) NOT NULL UNIQUE,
  `password` VARCHAR(255) NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

-- 3. Create Specialist Table
CREATE TABLE `specialist` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `specialist_name` VARCHAR(255) NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

-- 4. Create Doctor Table
CREATE TABLE `doctor` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `fullName` VARCHAR(255) NOT NULL,
  `dateOfBirth` VARCHAR(50) NOT NULL,
  `qualification` VARCHAR(255) NOT NULL,
  `specialist` VARCHAR(255) NOT NULL,
  `email` VARCHAR(255) NOT NULL UNIQUE,
  `phone` VARCHAR(20) NOT NULL,
  `password` VARCHAR(255) NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

-- 5. Create Appointment Table
CREATE TABLE `appointment` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `userId` INT NOT NULL,
  `fullName` VARCHAR(255) NOT NULL,
  `gender` VARCHAR(10) NOT NULL,
  `age` VARCHAR(10) NOT NULL,
  `appointmentDate` VARCHAR(50) NOT NULL,
  `email` VARCHAR(255) NOT NULL,
  `phone` VARCHAR(20) NOT NULL,
  `diseases` VARCHAR(255) NOT NULL,
  `doctorId` INT NOT NULL,
  `address` VARCHAR(255) NOT NULL,
  `status` VARCHAR(255) NOT NULL,
  PRIMARY KEY (`id`),
  FOREIGN KEY (`userId`) REFERENCES `user_details` (`id`) ON DELETE CASCADE,
  FOREIGN KEY (`doctorId`) REFERENCES `doctor` (`id`) ON DELETE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
