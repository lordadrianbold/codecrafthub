#CodeCraftHub API
Project overview: A simple, beginner-friendly REST API built with Node.js and Express to track learning courses. Data is stored in a single JSON file (courses.json) instead of a database. No authentication or user management—ideal for learning REST basics and file-based persistence.

Features
Create, read, update, and delete (CRUD) courses via REST endpoints
Data persisted to a JSON file named courses.json (auto-created if missing)
Each course fields:
id: auto-generated starting from 1
name: required
description: required
target_date: required, format YYYY-MM-DD
status: required, one of Not Started, In Progress, Completed
created_at: auto-generated timestamp when the course is created
Basic error handling:
Missing required fields
Invalid date format
Invalid status values
File read/write errors
Beginner-friendly code structure and comments
Server runs on port 5000
Installation
Prerequisites:

Node.js (LTS version recommended)
Setup steps:

Clone or copy the project files to your machine.
Open a terminal in the project root.
Install dependencies:
npm install
Start the server:
npm start
The server will run on http://localhost:5000
Note: The app.js (or equivalent entry point) will automatically create courses.json if it doesn't exist.

How to run the application
Start the server:
npm start
Verify it’s running by visiting:
http://localhost:5000/api/courses
You can also use curl or Postman to test the API.
API endpoint documentation
Base path: /api

Note: All endpoints for individual courses use the id path parameter (e.g., /api/courses/1).

POST /api/courses

Purpose: Add a new course

Request body (JSON):

name: string (required)
description: string (required)
target_date: string in YYYY-MM-DD (required)
status: one of "Not Started", "In Progress", "Completed" (required)
Response:

201 Created with the new course object (including id and created_at)
400 Bad Request if validation fails
500 Internal Server Error for file I/O issues
Example request: { "name": "Intro to Node.js", "description": "Learn Node basics", "target_date": "2026-04-30", "status": "Not Started" }

Example response: { "id": 1, "name": "Intro to Node.js", "description": "Learn Node basics", "target_date": "2026-04-30", "status": "Not Started", "created_at": "2026-03-30T12:34:56.789Z" }

GET /api/courses

Purpose: Get all courses
Response: 200 OK with an array of course objects
Example response: [ { "id": 1, "name": "Intro to Node.js", "description": "Learn Node basics", "target_date": "2026-04-30", "status": "Not Started", "created_at": "2026-03-30T12:34:56.789Z" } ]
GET /api/courses/:id

Purpose: Get a specific course by id
Response:
200 OK with the course object
404 Not Found if the course does not exist
Example response (200): { "id": 1, "name": "Intro to Node.js", "description": "Learn Node basics", "target_date": "2026-04-30", "status": "Not Started", "created_at": "2026-03-30T12:34:56.789Z" }
PUT /api/courses/:id

Purpose: Full update of a course (all fields required)
Request body (JSON): must include all fields
name, description, target_date (YYYY-MM-DD), status
Validations:
target_date must be a valid date in YYYY-MM-DD
status must be one of Not Started, In Progress, Completed
Response:
200 OK with the updated course
400 Bad Request for validation errors
404 Not Found if the course does not exist
Example request: { "name": "Intro to Node.js", "description": "Updated description", "target_date": "2026-05-15", "status": "In Progress" }
PATCH /api/courses/:id

Purpose: Partial update of a course (any subset of fields)
Request body: any of the fields (name, description, target_date, status)
Validations:
If target_date is provided, it must be a valid date in YYYY-MM-DD
If status is provided, it must be one of Not Started, In Progress, Completed
Response:
200 OK with the updated course
400 Bad Request for validation errors
404 Not Found if the course does not exist
Example request (partial): { "status": "Completed" }
DELETE /api/courses/:id

Purpose: Delete a course
Response:
204 No Content on success
404 Not Found if the course does not exist
Notes:

IDs are auto-generated starting at 1 based on existing entries.
created_at is automatically set when a course is created and preserved on updates.
Troubleshooting
Server not starting or port in use
Ensure no other process is using port 5000.
Try changing PORT in environment or process manager settings.
Data file cannot be created or written
Check file system permissions in the project directory.
Ensure the project root is writable.
Malformed JSON in courses.json
The API will attempt to reset the file to an empty array if it detects invalid JSON. If you see unexpected behavior, delete or repair courses.json and restart the server.
Validation errors without guidance
Review the error messages returned by the API (e.g., missing fields, invalid date format, invalid status) and adjust your request payload accordingly.
Date validation issues
target_date must be exactly in YYYY-MM-DD format and represent a real date (e.g., 2026-02-29 is invalid in non-leap years).
No authentication or user management
This project is intentionally simple for learning REST basics. If you need multi-user support, consider adding authentication and a database.
If you’d like, I can tailor the README with additional examples, a quick-start script, or a sample data set to bootstrap your local environment.
