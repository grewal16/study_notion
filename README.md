# 🚀 StudyNotion: Your Next-Gen E-Learning Platform

<p align="center"><img src="./src/assets/Logo/Logo-Full-Dark.png" alt="StudyNotion Logo" width="300"></p>

## Short Description
StudyNotion is a cutting-edge MERN stack-based e-learning platform designed to empower both instructors and students. It provides a robust environment for creating, managing, and consuming online courses, complete with secure authentication, payment integration, and real-time progress tracking. Dive into a world of knowledge with StudyNotion's intuitive and feature-rich interface!

## ✨ Key Features
*   **Dynamic Course Management:** Instructors can effortlessly create, edit, and categorize courses, adding sections, subsections, and rich media content.
*   **Secure User Authentication:** Implements comprehensive user authentication flows including signup, login, OTP verification, and password reset with role-based access for Students, Instructors, and Admins.
*   **Integrated Payment Gateway:** Seamless and secure course enrollment transactions powered by Razorpay for a smooth purchasing experience.
*   **Personalized Dashboards:** Tailored dashboards for students to track course progress and enrolled courses, and for instructors to manage their content and view analytics.
*   **Interactive Learning Experience:** Engaging video lectures, detailed course content, and the ability to mark course sections as complete.
*   **Comprehensive Rating & Review System:** Students can provide valuable feedback through ratings and reviews, contributing to course quality and transparency.
*   **Rich User Profiles:** Users can manage and update their personal profiles, including profile pictures and contact details.
*   **Automated Email Notifications:** Keep users informed with automated emails for course enrollments, payment confirmations, password updates, and contact form responses.
*   **Cloud-based Media Storage:** Leverages Cloudinary for efficient and scalable storage of course thumbnails and video content.

## Who is this for?
*   **Aspiring Educators & Experts:** If you're passionate about sharing knowledge, StudyNotion provides all the tools you need to create and sell your online courses to a global audience.
*   **Eager Learners:** Discover a vast array of courses across various categories, track your progress, and learn new skills at your own pace.
*   **Developers & Tech Enthusiasts:** Explore a modern MERN stack application with robust features, clean architecture, and best-in-class third-party integrations.

## Technology Stack & Architecture
StudyNotion is built on a powerful and scalable MERN (MongoDB, Express.js, React.js, Node.js) stack, incorporating modern tools and practices:

*   **Frontend:**
    *   **React.js:** A declarative, component-based JavaScript library for building interactive user interfaces.
    *   **Redux Toolkit:** Efficient state management for a seamless user experience.
    *   **Tailwind CSS:** A utility-first CSS framework for rapid and responsive UI development.
*   **Backend:**
    *   **Node.js & Express.js:** A robust and high-performance server-side runtime and framework for building RESTful APIs.
    *   **MongoDB:** A flexible NoSQL database to store and manage course data, user profiles, and more.
    *   **JWT (JSON Web Tokens):** For secure and stateless authentication.
*   **Cloud & Services:**
    *   **Cloudinary:** Cloud-based media management for image and video uploads.
    *   **Razorpay:** Integrated payment gateway for secure online transactions.
    *   **Nodemailer (inferred):** For sending transactional emails.

## 📊 Architecture & Database Schema

**Overall Architecture Diagram**
<p align="center"><img src="./images/architecture.png" alt="Architecture Diagram" width="700"></p>

**Database Schema (ERD)**
```mermaid
erDiagram
    "User" {
        string "ID"
        string "email"
        string "type"
    }
    "Profile" {
        string "ID"
        string "gender"
    }
    "Category" {
        string "ID"
        string "name"
    }
    "Course" {
        string "ID"
        string "name"
        number "price"
    }
    "Section" {
        string "ID"
        string "name"
    }
    "SubSection" {
        string "ID"
        string "title"
    }
    "Rating" {
        string "ID"
        number "value"
    }
    "Progress" {
        string "ID"
        array "videos"
    }
    "OTP" {
        string "ID"
        string "code"
    }

    "User" ||--o{ "Profile" : "has"
    "User" ||--o{ "Course" : "instructs"
    "User" }|--|| "Course" : "enrolls_in"
    "Category" ||--o{ "Course" : "defines"
    "Course" ||--o{ "Section" : "contains"
    "Section" ||--o{ "SubSection" : "has"
    "User" ||--o{ "Rating" : "gives"
    "Course" ||--o{ "Rating" : "gets"
    "User" ||--o{ "Progress" : "monitors"
    "Course" ||--o{ "Progress" : "for"
    "Progress" }|--|| "SubSection" : "marks_done"
```

## ⚡ Quick Start Guide

Follow these steps to get StudyNotion up and running on your local machine.

1.  **Prerequisites**
    *   Ensure you have Node.js (v14 or higher recommended) and npm installed.
    *   A running MongoDB instance (local or cloud-hosted like MongoDB Atlas).

2.  **Clone the Repository**
    ```bash
    git clone https://github.com/grewal16/study_notion.git
    cd study_notion
    ```

3.  **Install Dependencies**
    *   **For the Client (Frontend):**
        ```bash
        npm install
        ```
    *   **For the Server (Backend):**
        ```bash
        cd server
        npm install
        cd .. # Go back to the root directory
        ```

4.  **Environment Variables**
    *   Create a `.env` file in the `server/` directory.
    *   Populate it with your specific configurations. Example:
        ```env
        PORT=4000
        MONGO_URL="mongodb://localhost:27017/studynotion"
        JWT_SECRET="YOUR_JWT_SECRET_KEY"
        CLOUDINARY_CLOUD_NAME="your_cloud_name"
        CLOUDINARY_API_KEY="your_api_key"
        CLOUDINARY_API_SECRET="your_api_secret"
        MAIL_USER="your_email@example.com"
        MAIL_PASS="your_email_password_or_app_password"
        RAZORPAY_KEY_ID="rzp_test_YOUR_KEY_ID"
        RAZORPAY_KEY_SECRET="YOUR_RAZORPAY_SECRET"
        ```

5.  **Run the Application**
    *   **Start the Backend Server:**
        ```bash
        cd server
        npm start
        ```
        The server will typically run on `http://localhost:4000` (or your configured PORT).
    *   **Start the Frontend Application:**
        ```bash
        cd .. # If you are still in the server directory
        npm start
        ```
        The frontend will typically open in your browser at `http://localhost:3000`.

## 📜 License
License information was not specified in the provided repository data.
