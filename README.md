🚀 study_notion
Struggling to build a modern, full-featured online learning platform? Study Notion is a game-changing EdTech project, providing a complete MERN stack solution for instructors and students. This repository offers a robust foundation for creating, managing, and selling educational content, complete with secure payments, progress tracking, and media management.

✨ Key Features
👨‍🎓 Complete Student Lifecycle: Features a full student dashboard, course catalog, shopping cart, and progress tracking, powered by React.js and Redux Toolkit.

🧑‍🏫 Powerful Instructor Tools: Instructors can create, edit, and manage courses, sections, and video content through a dedicated dashboard.

💳 Secure Payment Integration: Seamlessly handles course purchases using a pre-configured Razorpay integration.

🔐 Robust User Authentication: Implements a secure authentication system with JWT, OTP verification, and role-based access control using Node.js and Express.js middleware.

🖼️ Cloud Media Management: Efficiently handles video and image uploads for course content using Cloudinary.

⭐ Rating and Review System: Allows students to provide valuable feedback on courses, creating a dynamic and interactive community.

Who is this for?
Developers looking for a comprehensive, production-ready MERN stack project to use as a boilerplate for a modern EdTech application.

Instructors & Educators who need a platform to host and sell their courses, complete with student management and payment processing.

Students of web development who want to explore a large-scale, real-world application built with best practices in mind.

Technology Stack & Architecture
Core Technologies: MongoDB, Express.js, React.js, Node.js (MERN Stack), Tailwind CSS.

Services & APIs: Razorpay for payments, Cloudinary for media storage, Nodemailer for email services.

State Management: Redux Toolkit for efficient and predictable state management on the frontend.

Architecture Summary:
Study Notion is a classic client-server application. The backend, built with Node.js and Express.js, follows a layered architecture (Routes -> Controllers -> Models) to provide a robust REST API. The frontend is a responsive single-page application (SPA) built with React.js, which consumes this API to deliver a seamless user experience for students and instructors.

📊 Architecture & Database Schema
Code snippet

erDiagram
    USER {
        string firstName
        string lastName
        string email
        string password
        string accountType
        string image
        string token
        array courses
    }
    PROFILE {
        string dateOfBirth
        string about
        string contactNumber
        string gender
    }
    COURSE {
        string courseName
        string courseDescription
        string instructor
        string price
        string thumbnail
        array studentsEnrolled
    }
    SECTION {
        string sectionName
        array subSections
    }
    SUB_SECTION {
        string title
        string timeDuration
        string description
        string videoUrl
    }
    RATING_AND_REVIEW {
        string user
        integer rating
        string review
    }
    CATEGORY {
        string name
        string description
        array courses
    }

    USER ||--|{ PROFILE : "has one"
    USER ||--o{ COURSE : "can enroll in many"
    USER ||--o{ RATING_AND_REVIEW : "gives"
    COURSE ||--|{ SECTION : "contains"
    COURSE ||--o{ RATING_AND_REVIEW : "receives"
    COURSE }o--|| CATEGORY : "belongs to"
    SECTION ||--|{ SUB_SECTION : "contains"

⚡ Quick Start Guide
Clone the Repository:

Bash

git clone https://github.com/grewal16/study_notion.git
cd study_notion
Install Dependencies:
Install dependencies for both the server and the client.

Bash

# Install server dependencies
cd server && npm install
# Install client dependencies
cd ../ && npm install
Setup Environment Variables:
Create a .env file in the server/config/ directory and add your MongoDB URI, JWT secret, and API keys for Cloudinary and Razorpay.

Run the Application:
Start both the backend and frontend servers.

Bash

# Start the backend server (from the server folder)
npm start
# Start the frontend app (from the root folder)
npm start
