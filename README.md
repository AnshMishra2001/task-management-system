# Task Management System Specification (Version 1.0)

## Overview
The Task Management System is a web-based single-page application (SPA) that enables users to manage tasks efficiently. Users can create, view, update, and delete tasks, each with a title, description, status, and optional due date. The system comprises a RESTful backend API and a React-based frontend, designed for simplicity and scalability.

## Functional Requirements
1. **Task Creation**: Users can create a task with a title, description, status, and optional due date.
2. **Task Listing**: Users can view a list of all tasks, including an empty list if no tasks exist.
3. **Task Details**: Users can view details of a specific task by its ID.
4. **Task Update**: Users can modify an existing task’s details.
5. **Task Deletion**: Users can delete a task by its ID.
6. **Input Validation**: The system enforces constraints on task data (e.g., title length, valid status values).

## API Details
The backend provides RESTful API endpoints returning JSON. Standard HTTP status codes (e.g., 200 OK, 400 Bad Request) indicate success or failure.

### Endpoints
1. **Create Task**
   - **Method**: `POST`
   - **Path**: `/tasks`
   - **Request Body**:
     ```json
     {
       "title": "string (required, 1–100 characters)",
       "description": "string (optional, 0–500 characters)",
       "status": "string (required, one of: 'To Do', 'In Progress', 'Done')",
       "dueDate": "string (optional, ISO 8601, e.g., '2025-07-10')"
     }
     ```
   - **Response (201 Created)**:
     ```json
     {
       "id": number,
       "title": "string",
       "description": "string",
       "status": "string",
       "dueDate": "string|null"
     }
     ```
   - **Example Response (201 Created)**:
     ```json
     {
       "id": 1,
       "title": "Finish project",
       "description": "Complete the coding evaluation",
       "status": "To Do",
       "dueDate": "2025-07-10"
     }
     ```
   - **Error (400 Bad Request)**: Returns `{ "error": "string" }` (e.g., `{ "error": "Title is required" }`).

2. **List Tasks**
   - **Method**: `GET`
   - **Path**: `/tasks`
   - **Response (200 OK)**:
     ```json
     [
       {
         "id": number,
         "title": "string",
         "description": "string",
         "status": "string",
         "dueDate": "string|null"
       },
       ...
     ]
     ```
   - **Example Response (200 OK)**:
     ```json
     [
       {
         "id": 1,
         "title": "Finish project",
         "description": "Complete the coding evaluation",
         "status": "To Do",
         "dueDate": "2025-07-10"
       },
       {
         "id": 2,
         "title": "Review spec",
         "description": "",
         "status": "In Progress",
         "dueDate": null
       }
     ]
     ```
   - **Response (200 OK, Empty List)**:
     ```json
     []
     ```

3. **Get Task**
   - **Method**: `GET`
   - **Path**: `/tasks/:id`
   - **Response (200 OK)**: Same as task object in Create Task.
   - **Example Response (200 OK)**:
     ```json
     {
       "id": 1,
       "title": "Finish project",
       "description": "Complete the coding evaluation",
       "status": "To Do",
       "dueDate": "2025-07-10"
     }
     ```
   - **Error (404 Not Found)**: Returns `{ "error": "Task not found" }`.

4. **Update Task**
   - **Method**: `PUT`
   - **Path**: `/tasks/:id`
   - **Request Body**: Same as Create Task (all fields optional).
   - **Response (200 OK)**: Updated task object.
   - **Example Response (200 OK)**:
     ```json
     {
       "id": 1,
       "title": "Finish project",
       "description": "Updated description",
       "status": "In Progress",
       "dueDate": "2025-07-15"
     }
     ```
   - **Error (404 Not Found)**: Returns `{ "error": "Task not found" }`.
   - **Error (400 Bad Request)**: Returns `{ "error": "string" }` (e.g., `{ "error": "Title exceeds 100 characters" }`).

5. **Delete Task**
   - **Method**: `DELETE`
   - **Path**: `/tasks/:id`
   - **Response (204 No Content)**: No body on success.
   - **Error (404 Not Found)**: Returns `{ "error": "Task not found" }`.

## UI Requirements
The frontend is a React-based SPA with the following components:

### Task List
- Displays tasks in a table with columns: Title, Status, Due Date, Actions (Edit, Delete buttons).
- Shows “No tasks available” if the task list is empty.

### Task Form
- **Fields**:
  - Title (text input)
  - Description (textarea)
  - Status (dropdown: “To Do,” “In Progress,” “Done”)
  - Due Date (date picker)
- **Buttons**:
  - Submit (Create/Update)
  - Cancel (clears form or navigates back to task list)

### Error Handling
- Displays inline errors for invalid inputs (e.g., “Title is required” below the title field).

### Navigation
- A “New Task” button routes to the task form.

### Text-Based Wireframe
```
[Header: Task Management System | New Task Button]
[Task List]
-------------------------------------------------
| Title          | Status      | Due Date | Actions |
-------------------------------------------------
| Task 1         | To Do       | 2025-07-10 | Edit | Delete |
| Task 2         | In Progress | -        | Edit | Delete |
-------------------------------------------------
[No tasks available (if empty)]

[Task Form (on New Task or Edit)]
Title: [Text Input]
Description: [Textarea]
Status: [Dropdown: To Do | In Progress | Done]
Due Date: [Date Picker]
[Submit Button] [Cancel Button]
[Error: Title is required (if applicable)]
```

## Validation Rules
- **Title**: Required, 1–100 characters, non-whitespace only.  
  **Error Messages**:  
  - “Title is required”  
  - “Title must not exceed 100 characters”  
  - “Title cannot be only whitespace”
- **Description**: Optional, 0–500 characters.  
  **Error Message**:  
  - “Description must not exceed 500 characters”
- **Status**: Required, must be “To Do,” “In Progress,” or “Done.”  
  **Error Message**:  
  - “Invalid status”
- **Due Date**: Optional, valid ISO 8601 date (e.g., “2025-07-10”).  
  **Error Message**:  
  - “Invalid date format”

## Notes
- The system handles edge cases (e.g., empty task list, invalid inputs) gracefully.
- No user authentication is required for this version.
- Future iterations may include bulk task deletion, task filtering, or user roles.
