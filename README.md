# Student Management REST API

Spring Boot 3 (Java 17) REST API to manage student records, using Spring Data JPA and MySQL.

## Student entity
| Field | Type | Rules |
|---|---|---|
| id | Long | Primary key, auto-generated |
| name | String | required, max 100 chars |
| email | String | required, valid email, unique |
| course | String | required |
| age | Integer | required, 1–120 |

## Endpoints
| Method | URL | Success | Errors |
|---|---|---|---|
| POST | `/api/students` | 201 Created | 400 validation, 409 duplicate email |
| GET | `/api/students` | 200 OK | – |
| GET | `/api/students/{id}` | 200 OK | 404 not found |
| PUT | `/api/students/{id}` | 200 OK | 400, 404, 409 |
| DELETE | `/api/students/{id}` | 204 No Content | 404 |
| GET | `/api/students/course/{course}` | 200 OK (empty list if none) | – |

Error body example:
```json
{ "timestamp": "...", "status": 404, "error": "Not Found",
  "message": "Student not found with id: 99", "path": "/api/students/99", "fieldErrors": null }
```

## Database configuration
Edit `src/main/resources/application.properties` and set your MySQL username/password
(defaults: `root` / `root`). The `student_db` database and `students` table are created automatically.

## Run
```bash
mvn spring-boot:run
```
API base URL: `http://localhost:8080/api/students`

## Testing with Postman
Import `postman/Student_Management_API.postman_collection.json`, then run the requests in order
(Add → Get all → Get by id → Update → Get by course → Delete → Get deleted (404)) and take screenshots.
Sample body:
```json
{ "name": "Aarav Sharma", "email": "aarav@example.com", "course": "Computer Science", "age": 20 }
```

## Project structure
```
com.school.studentapi
├── controller/  StudentController
├── service/     StudentService
├── repository/  StudentRepository
├── entity/      Student
└── exception/   StudentNotFoundException, DuplicateEmailException, ErrorResponse, GlobalExceptionHandler
```
