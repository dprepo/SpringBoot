JWT authentication in a Spring Boot 3 application
JSON Web Tokens (JWT). It provides a flexible and stateless way to verify the identity of users and secure API endpoints; it is also called Token-Based Authentication.

API route	Access status	Description
[POST] /auth/signup	Unprotected	Register a new user
[POST] /auth/login	Unprotected	Authenticate a user
[GET] /users/me	Protected	Retrieve the current authenticated user
[GET] /users	Protected	Retrieve all the users

Set up the project
The Spring Boot project needs these four dependencies:
The Spring Web: to build Web, including RESTful applications using Spring MVC. It uses Apache Tomcat as the default embedded container.
The Spring Security: Allows implementing authentication and access-based control.
The Spring Data JPA: Persist data in SQL stores with Java Persistence API using Spring Data and Hibernate.
MySQL Driver for Java: The MySQL driver makes it possible to interact with a database from a Java application.

-----------------------------------
1. signup API 
---------------------------------------
http://localhost:8005/auth/signup
method: post
req: {
    "email":"dineshpandit@gmail.com",
    "password":"qwerty",
    "fullName":"Dinesh pandit"
}
Response: 
{
    "id": 1,
    "fullName": "Dinesh pandit",
    "email": "dineshpandit@gmail.com",
    "password": "$2a$10$EkfJFk8hFYCnKlwT4sZYvO7xQgUUNhLBIguV29ksGCtq2lo2Mpc96",
    "createdAt": "2024-09-01T15:40:46.053+00:00",
    "updatedAt": "2024-09-01T15:40:46.053+00:00",
    "enabled": true,
    "authorities": [],
    "username": "dineshpandit@gmail.com",
    "accountNonLocked": true,
    "credentialsNonExpired": true,
    "accountNonExpired": true
}

-----------------------------------
2. login API 
-----------------------------------
URL : http://localhost:8005/auth/login
request:
 {
    "email":"dineshpandit@gmail.com",
    "password":"qwerty"
}
response: 
{
    "token": "eyJhbGciOiJIUzI1NiJ9
              .eyJzdWIiOiJkaW5lc2hwYW5kaXRAZ21haWwuY29tIiwiaWF0IjoxNzI1MjA2NjUyLCJleHAiOjE3MjUyOTMwNTJ9
              .FJkSwvQC7WMtMr4TiA5kUHwHxfWg3p-nsZAWBsZGevE",
    "expiresIn": 86400000
}

-----------------------------------
3. users API 
-----------------------------------
URL : http://localhost:8005/users
Http Method: GET
request: Header -> Authorization -> Bearer Token -> eyJhbGciOiJIUzI1NiJ9
              .eyJzdWIiOiJkaW5lc2hwYW5kaXRAZ21haWwuY29tIiwiaWF0IjoxNzI1MjA2NjUyLCJleHAiOjE3MjUyOTMwNTJ9
              .FJkSwvQC7WMtMr4TiA5kUHwHxfWg3p-nsZAWBsZGevE
 Response :
  [
    {
        "id": 1,
        "fullName": "Dinesh pandit",
        "email": "dineshpandit@gmail.com",
        "password": "$2a$10$EkfJFk8hFYCnKlwT4sZYvO7xQgUUNhLBIguV29ksGCtq2lo2Mpc96",
        "createdAt": "2024-09-01T15:40:46.053+00:00",
        "updatedAt": "2024-09-01T15:40:46.053+00:00",
        "enabled": true,
        "accountNonLocked": true,
        "username": "dineshpandit@gmail.com",
        "authorities": [],
        "accountNonExpired": true,
        "credentialsNonExpired": true
    }
]
