# Task Management System

# Overview
The Task Management Application allows users to manage tasks via a web interface. Users can perfrom CRUD operations (Create, Read, Update, Delete) each with title, description, status and an optional due date. This application comprises of a backend API and frontend user interface to support efficient task management for users.

## Functional Requirements
1. **Task Creation**: Users can create a new task with a title, description, status, and optional due date.
2. **Task Listing**: Users can view a list of all tasks.
3. **Task Details**: Users can view details of a specific task.
4. **Task Update**: Users can update an existing task’s details.
5. **Task Deletion**: Users can delete a redundant task.
6. **Input Validation**: The system enforces rules on task data (e.g., title length, valid status).

## API Details
The backend provides RESTful API endpoints to support task management. All endpoints return JSON and use standard HTTP status codes (e.g., 200 for success, 400 for bad requests).

### Example: Create Task

**Method:** POST  
**Path:** `/tasks`

#### Response (201 Created)
```json
{
  "id": number,
  "title": "string",
  "description": "string",
  "status": "string",
  "dueDate": "string|null"
}
```


## UI Requirements

The frontend is a **React-based SPA** with the following components:

### Task List
- Displays tasks in a table with columns:
  - **Title**
  - **Status**
  - **Due Date**
  - **Actions** (Edit, Delete buttons)
- Shows **“No tasks available”** if the task list is empty.

### Task Form
- **Fields:**
  - Title (text input)
  - Description (textarea)
  - Status (dropdown: “To Do,” “In Progress,” “Done”)
  - Due Date (date picker)
- **Buttons:**
  - Submit (Create/Update)
  - Cancel (clears form or navigates back)

### Error Handling
- Displays inline errors for invalid inputs (e.g., **“Title is required”** below the title field).

### Navigation
- A **“New Task”** button links to the task form.

## Validation Rules

- **Title:** Required, 1–100 characters.  
  **Error Messages:**  
  - "Title is required"  
  - "Title must not exceed 100 characters."

- **Description:** Optional, 0–500 characters.  
  **Error Message:**  
  - "Description must not exceed 500 characters."

- **Status:** Required, must be "To Do," "In Progress," or "Done."  
  **Error Message:**  
  - "Invalid status."

- **Due Date:** Optional, valid ISO 8601 date (e.g., "2025-07-10").  
  **Error Message:**  
  - "Invalid date format."




