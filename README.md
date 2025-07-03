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

[Header: Task Management App | New Task Button]

[Task List]
-------------------------------------------------
| Title          | Status      | Due Date   | Actions       |
-------------------------------------------------
| Task 1         | To Do       | 2025-07-10 | Edit | Delete |
| Task 2         | In Progress | -          | Edit | Delete |
-------------------------------------------------
[No tasks available (if empty)]

[Task Form (on New Task or Edit)]
Title: [Text Input]
Description: [Textarea]
Status: [Dropdown: To Do | In Progress | Done]
Due Date: [Date Picker]
[Submit Button] [Cancel Button]
[Error: Title is required (if applicable)]


