# 🚀 StudyNotion: Your All-in-One E-Learning Platform

<p align="center"><img src="./src/assets/Logo/Logo-Full-Dark.png" alt="StudyNotion Logo" width="300"></p>

## Short Description

StudyNotion is a cutting-edge, comprehensive full-stack e-learning platform meticulously designed to empower both educators and learners. It provides a robust, intuitive environment for instructors to create and manage courses, and for students to explore, enroll in, and track their educational journey. With features ranging from secure authentication and payment integration to rich content management and progress tracking, StudyNotion transforms the way knowledge is shared and acquired online.

## ✨ Key Features

*   **Secure User Authentication & Authorization:** Robust JWT-based authentication system with dedicated roles for Students, Instructors, and Administrators, ensuring secure access and personalized experiences. Includes features for OTP-based email verification and password reset.
*   **Dynamic Course Management:** Instructors can effortlessly create, edit, publish, and manage multi-sectional courses, complete with sub-sections, video lectures, descriptions, and prerequisites.
*   **Rich Content Management:** Supports multimedia content (e.g., video uploads via Cloudinary) within course sub-sections, enabling engaging and diverse learning materials.
*   **Category-Based Course Organization:** Courses are categorized, allowing students to easily discover content relevant to their interests.
*   **Seamless Payment Integration:** Integrated with Razorpay for secure and smooth course enrollment payments, providing a frictionless purchasing experience.
*   **Personalized Dashboards:** Dedicated dashboards for students to track their enrolled courses and progress, and for instructors to monitor their course performance, earnings, and student engagement.
*   **Interactive Rating & Review System:** Students can leave ratings and reviews for courses, providing valuable feedback for instructors and guidance for prospective learners.
*   **Comprehensive User Profiles:** Manage and update personal details, profile pictures, and account settings with ease.
*   **Automated Email Notifications:** Keeps users informed with automated emails for course enrollment, password updates, payment confirmations, and contact form responses.
*   **Responsive & Intuitive UI:** Built with React and styled using Tailwind CSS, offering a modern, accessible, and highly responsive user interface across all devices.

## Who is this for?

*   **Aspiring Students:** Those eager to learn new skills, explore diverse subjects, and progress their careers through high-quality online courses.
*   **Passionate Educators & Instructors:** Individuals looking for a platform to share their expertise, create engaging courses, and reach a global audience with powerful content management tools.
*   **Educational Institutions:** Organizations seeking a scalable and secure platform to host their online curriculum and manage student/instructor interactions.
*   **Developers:** A fantastic reference for building full-stack applications with React, Node.js, Express, MongoDB, and integrating various third-party services.

## Technology Stack & Architecture

StudyNotion is built on a robust and scalable MERN stack, leveraging modern web technologies to deliver a high-performance e-learning experience.

*   **Frontend:**
    *   **React.js:** A declarative, component-based JavaScript library for building dynamic user interfaces.
    *   **Redux Toolkit:** For efficient and predictable state management across the application.
    *   **Tailwind CSS:** A utility-first CSS framework for rapidly building custom designs.
*   **Backend:**
    *   **Node.js:** A JavaScript runtime for building scalable server-side applications.
    *   **Express.js:** A fast, unopinionated, minimalist web framework for Node.js.
    *   **JWT (JSON Web Tokens):** For secure, stateless authentication.
*   **Database:**
    *   **MongoDB:** A flexible NoSQL document database, managed using **Mongoose** ODM.
*   **Cloud Services:**
    *   **Cloudinary:** For efficient cloud-based image and video management (course thumbnails, video lectures, profile pictures).
    *   **Razorpay:** For secure and seamless payment gateway integration.
    *   **Nodemailer:** For sending automated email notifications.

## 📊 Architecture & Database Schema

The platform's architecture follows a typical client-server model with a well-structured database schema to support complex relationships between users, courses, and educational content.

```mermaid
erDiagram
    OTP {
        string "email"
        string "otp"
        datetime "createdAt"
    }
    User {
        string "firstName"
        string "lastName"
        string "email"
        string "password"
        string "accountType" "ENUM('Admin', 'Student', 'Instructor')"
        objectId "additionalDetails_FK" "refers to Profile"
        objectId[] "courses_FK" "refers to Course for student/instructor"
        objectId[] "courseProgress_FK" "refers to CourseProgress"
        string "image" "Cloudinary URL"
        string "token" "for password reset"
        datetime "resetPasswordExpires"
        boolean "active" "account status"
    }
    Profile {
        string "gender"
        date "dateOfBirth"
        string "about"
        string "contactNumber"
    }
    Category {
        string "name"
        string "description"
        objectId[] "courses_FK" "refers to Course"
    }
    Course {
        string "courseName"
        string "courseDescription"
        objectId "instructor_FK" "refers to User (Instructor)"
        string "whatYouWillLearn"
        objectId[] "courseContent_FK" "refers to Section"
        objectId[] "ratingAndReviews_FK" "refers to RatingAndReview"
        number "price"
        string "thumbnail" "Cloudinary URL"
        objectId "category_FK" "refers to Category"
        objectId[] "studentsEnrolled_FK" "refers to User (Student)"
        string[] "instructions"
        string "status" "ENUM('Draft', 'Published')"
        datetime "createdAt"
    }
    Section {
        string "sectionName"
        objectId[] "subSection_FK" "refers to SubSection"
    }
    SubSection {
        string "title"
        string "timeDuration"
        string "description"
        string "videoUrl" "Cloudinary URL"
    }
    RatingAndReview {
        objectId "user_FK" "refers to User (Student)"
        number "rating"
        string "review"
        objectId "course_FK" "refers to Course"
        datetime "createdAt"
    }
    CourseProgress {
        objectId "courseID_FK" "refers to Course"
        objectId "userId_FK" "refers to User (Student)"
        objectId[] "completedVideos_FK" "refers to SubSection"
    }

    User ||--o{ Profile : "has a profile"
    User ||--o{ Course : "teaches/enrolls in"
    User ||--o{ CourseProgress : "tracks progress"
    User ||--o{ RatingAndReview : "submits"
    Course ||--o{ Category : "belongs to"
    Course ||--o{ Section : "contains"
    Course ||--o{ RatingAndReview : "receives"
    Section ||--o{ SubSection : "includes"
    CourseProgress ||--o{ Course : "for"
    CourseProgress ||--o{ User : "by"
    CourseProgress ||--o{ SubSection : "completes"
```

## ⚡ Quick Start Guide

To get StudyNotion up and running on your local machine, follow these steps:

1.  **Clone the Repository:**
    ```bash
    git clone https://github.com/grewal16/study_notion.git
    cd study_notion
    ```

2.  **Install Dependencies:**
    Navigate to both the client (root) and server directories and install the required packages.

    ```bash
    # For the frontend (in the root directory)
    npm install
    # or yarn install

    # For the backend (in the server directory)
    cd server
    npm install
    # or yarn install
    cd .. # Go back to the root directory
    ```

3.  **Environment Configuration:**
    Create a `.env` file in both the root directory (for frontend environment variables, if any) and the `server` directory. Populate them with your respective credentials.

    **`server/.env` example:**
    ```
    MONGO_DB_URL="YOUR_MONGODB_CONNECTION_STRING"
    JWT_SECRET="YOUR_VERY_STRONG_JWT_SECRET"
    CLOUDINARY_CLOUD_NAME="YOUR_CLOUDINARY_CLOUD_NAME"
    CLOUDINARY_API_KEY="YOUR_CLOUDINARY_API_KEY"
    CLOUDINARY_API_SECRET="YOUR_CLOUDINARY_API_SECRET"
    MAIL_HOST="YOUR_MAIL_HOST"
    MAIL_USER="YOUR_MAIL_USER"
    MAIL_PASS="YOUR_MAIL_PASS"
    RAZORPAY_KEY_ID="YOUR_RAZORPAY_KEY_ID"
    RAZORPAY_KEY_SECRET="YOUR_RAZORPAY_KEY_SECRET"
    PORT=4000
    FRONTEND_URL="http://localhost:3000"
    ```

4.  **Run the Application:**

    ```bash
    # Start the backend server (from the root directory)
    cd server
    npm start # or 'npm run dev' if configured
    # In a new terminal, start the frontend
    cd .. # Go back to root
    npm start
    # or yarn start
    ```

    The frontend should now be running on `http://localhost:3000` and the backend on `http://localhost:4000` (or your configured ports).

## 📜 License

No specific license file was found in the repository's root directory. Please check the project's official repository or contact the author for licensing information.
