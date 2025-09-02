# Mermaid Test

```mermaid
erDiagram
    USER {
        string firstName
        string lastName
        string email
        string accountType
        string image
    }
    PROFILE {
        string dateOfBirth
        string about
        string gender
    }
    COURSE {
        string courseName
        string price
        string thumbnail
    }
    SECTION {
        string sectionName
    }
    SUB_SECTION {
        string title
        string description
        string videoUrl
    }
    RATING_AND_REVIEW {
        int rating
        string review
    }
    CATEGORY {
        string name
    }

    USER ||--|{ PROFILE : "has"
    USER ||--o{ COURSE : "enrolls in"
    USER ||--o{ RATING_AND_REVIEW : "creates"
    COURSE ||--|{ SECTION : "contains"
    COURSE }o--|| CATEGORY : "belongs to"
    COURSE ||--o{ RATING_AND_REVIEW : "has"
    SECTION ||--|{ SUB_SECTION : "contains"
