
# 🚀 StudyNotion

<p align="center"><img src="./src/assets/Logo/Logo-Full-Light.png" alt="StudyNotion Logo" width="250"></p>

## Short Description

StudyNotion is a cutting-edge, full-stack MERN (MongoDB, Express.js, React, Node.js) online learning platform designed to revolutionize the way education is delivered and consumed. It provides a robust and interactive ecosystem for both passionate instructors to craft and deliver engaging courses, and for ambitious learners to discover and master new skills. From secure authentication and comprehensive course management to seamless payment integration and real-time progress tracking, StudyNotion is engineered to provide a superior e-learning experience.

## ✨ Key Features

*   **Robust Authentication & Authorization:** Secure user registration, login, and password management with distinct roles for Students, Instructors, and Administrators, ensuring tailored experiences and access control.
*   **Dynamic Course Management:** Empower instructors to effortlessly create, update, delete, and publish courses with rich content, including sections, subsections, and video lectures, all hosted via Cloudinary.
*   **Seamless Enrollment & Payments:** Integrated with Razorpay for secure and efficient payment processing, allowing students to easily enroll in desired courses.
*   **Personalized User Dashboards:** Intuitive dashboards for students to track enrolled courses and progress, and for instructors to monitor course performance and student engagement.
*   **Comprehensive User Profiles:** Detailed user profiles with options to update personal information, change profile pictures, and manage account settings.
*   **Interactive Learning Experience:** Features like ratings and reviews allow students to provide feedback and help others discover quality content.
*   **Email Notifications:** Automated email services for account verification, course enrollment, payment confirmations, and password updates, keeping users informed.
*   **Responsive & Engaging UI:** A modern, visually appealing frontend built with React.js and styled with Tailwind CSS, offering a smooth user experience across devices.
*   **Category-Based Course Exploration:** Students can easily browse and discover courses across various categories, enhancing content discoverability.
*   **Media Management:** Utilizes Cloudinary for efficient storage and delivery of course videos and images, ensuring high performance.

## Who is this for?

*   **Aspiring Students:** Individuals eager to learn new skills or deepen their existing knowledge through a rich catalog of online courses.
*   **Passionate Educators/Instructors:** Experts and professionals looking to share their knowledge and build an audience by creating and managing their own courses.
*   **E-learning Entrepreneurs:** Visionaries seeking a robust and scalable platform to launch and operate their own online educational institution.
*   **Developers:** Those interested in a comprehensive MERN stack application showcasing best practices in full-stack development.

## Technology Stack & Architecture

StudyNotion leverages a powerful and modern technology stack to deliver a high-performance, scalable, and maintainable application:

*   **Frontend:** React.js, Redux Toolkit, React Router DOM, Tailwind CSS.
*   **Backend:** Node.js, Express.js.
*   **Database:** MongoDB (via Mongoose ODM).
*   **Cloud Services:** Cloudinary for media storage.
*   **Payment Gateway:** Razorpay.
*   **Email Service:** Nodemailer.
*   **Authentication:** JWT (JSON Web Tokens) for secure, stateless authentication.

## 📊 Architecture & Database Schema

The architecture is a classic client-server model, with a React frontend consuming RESTful APIs exposed by the Node.js/Express.js backend. Data is persisted in a MongoDB NoSQL database.

```mermaid
erDiagram
    "User" {
        ObjectId "_id" PK
        String "firstName"
        String "lastName"
        String "email"
        String "password"
        String "accountType" "Student, Instructor, Admin"
        ObjectId "additionalDetails" FK "Profile"
        String "image"
        ObjectId[] "courses" FK "Course" "Enrolled Courses"
        ObjectId[] "courseProgress" FK "CourseProgress"
        String "token"
        Date "resetPasswordExpires"
    }
    "Profile" {
        ObjectId "_id" PK
        String "gender"
        Date "dateOfBirth"
        Number "contactNumber"
        String "about"
    }
    "OTP" {
        ObjectId "_id" PK
        String "email"
        String "otp"
        Date "createdAt"
    }
    "Category" {
        ObjectId "_id" PK
        String "name"
        String "description"
        ObjectId[] "courses" FK "Course"
    }
    "Course" {
        ObjectId "_id" PK
        String "courseName"
        String "courseDescription"
        ObjectId "instructor" FK "User"
        String "whatYouWillLearn"
        String "thumbnail"
        Number "price"
        ObjectId[] "courseContent" FK "Section"
        ObjectId[] "ratingAndReviews" FK "RatingAndReview"
        ObjectId "category" FK "Category"
        ObjectId[] "studentsEnrolled" FK "User"
        String[] "instructions"
        String "status" "Draft, Published"
        Number "totalDuration"
    }
    "Section" {
        ObjectId "_id" PK
        String "sectionName"
        ObjectId[] "subSection" FK "SubSection"
    }
    "SubSection" {
        ObjectId "_id" PK
        String "title"
        Number "timeDuration"
        String "description"
        String "videoUrl"
    }
    "RatingAndReview" {
        ObjectId "_id" PK
        ObjectId "user" FK "User"
        ObjectId "course" FK "Course"
        Number "rating"
        String "review"
    }
    "CourseProgress" {
        ObjectId "_id" PK
        ObjectId "courseID" FK "Course"
        ObjectId "userID" FK "User"
        ObjectId[] "completedLectures" FK "SubSection"
    }

    "User" ||--o{ "Profile" : "has"
    "User" ||--|{ "OTP" : "verifies with"
    "User" ||--o{ "Course" : "creates/enrolls in"
    "Category" ||--o{ "Course" : "contains"
    "Course" ||--o{ "Section" : "includes"
    "Section" ||--o{ "SubSection" : "comprises"
    "Course" ||--o{ "RatingAndReview" : "receives"
    "User" ||--o{ "RatingAndReview" : "gives"
    "User" ||--o{ "CourseProgress" : "tracks"
    "Course" ||--o{ "CourseProgress" : "is_tracked_by"
    "CourseProgress" ||--o{ "SubSection" : "completes"
```

## ⚡ Quick Start Guide

To get StudyNotion up and running locally, follow these steps:

1.  **Prerequisites:**
    *   Node.js (v14.x or higher)
    *   npm or yarn package manager
    *   MongoDB (local instance or cloud service like MongoDB Atlas)
    *   Cloudinary Account
    *   Razorpay Account

2.  **Clone the Repository:**
    ```bash
    git clone https://github.com/grewal16/study_notion.git
    cd study_notion
    ```

3.  **Backend Setup:**
    ```bash
    cd server
    npm install # or yarn install
    ```
    Create a `.env` file in the `server` directory with the following variables (example placeholders):
    ```env
    MONGO_DB_URL=your_mongodb_connection_string
    JWT_SECRET=your_jwt_secret_key
    CLOUD_NAME=your_cloudinary_cloud_name
    API_KEY=your_cloudinary_api_key
    API_SECRET=your_cloudinary_api_secret
    MAIL_HOST=your_mail_host_smtp
    MAIL_USER=your_mail_user
    MAIL_PASS=your_mail_password
    RAZORPAY_KEY_ID=your_razorpay_key_id
    RAZORPAY_KEY_SECRET=your_razorpay_key_secret
    CORS_ORIGIN=http://localhost:3000 # Or your frontend URL
    PORT=4000
    ```
    Start the backend server:
    ```bash
    npm start # or yarn start
    ```

4.  **Frontend Setup:**
    ```bash
    cd ../ # navigate back to the root directory
    npm install # or yarn install
    ```
    Create a `.env` file in the root directory (for frontend):
    ```env
    REACT_APP_BASE_URL=http://localhost:4000/api/v1 # Or your backend API URL
    ```
    Start the frontend application:
    ```bash
    npm start # or yarn start
    ```

5.  **Access the Application:**
    Open your browser and navigate to `http://localhost:3000` (or the port where your React app is running). You're all set to explore StudyNotion!
