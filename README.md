Technical Documentation Exercises
Exercise A: User Manual Procedure
Setting Up a GitHub Repository and Making a First Commit

This guide explains how a beginner can create a GitHub repository, create a local Git repository, make a first commit, and upload the commit to GitHub.

Prerequisites

Before starting, the reader needs:

A computer running Windows, macOS, or Linux.

An internet connection.

A web browser.

A GitHub account.

Git installed on the computer.

A text editor.

Basic knowledge of opening and using a terminal or command prompt.

Step-by-Step Procedure
Step 1: Open GitHub

Action: Open https://github.com in a web browser.

Expected result: The GitHub website appears.

Step 2: Sign in to GitHub

Action: Select Sign in and enter your GitHub account credentials.

Expected result: Your GitHub account opens.

Step 3: Start creating a repository

Action: Select the + button in the upper-right corner and select New repository.

Expected result: The repository creation page appears.

Step 4: Enter the repository name

Action: Enter my-first-project as the repository name.

Expected result: The repository name appears in the repository name field.

Step 5: Select the repository visibility

Action: Select Public as the repository visibility.

Expected result: The repository is configured as public.

Step 6: Create the repository

Action: Select Create repository.

Expected result: GitHub displays the newly created repository.

Step 7: Open a terminal

Action: Open a terminal or command prompt on the computer.

Expected result: A command-line window appears with a command prompt.

Step 8: Create the project directory

Action: Run mkdir my-first-project.

Expected result: A directory named my-first-project is created.

Step 9: Enter the project directory

Action: Run cd my-first-project.

Expected result: The terminal is now operating inside the project directory.

Step 10: Initialize Git

Action: Run git init.

Expected result: Git creates a local repository in the project directory.

Step 11: Create the README file

Action: Create a file named README.md inside the project directory.

Expected result: The project directory contains README.md.

Step 12: Add content to the README

Action: Add # My First Project to README.md.

Expected result: The README contains the project heading.

Step 13: Check the repository status

Action: Run git status.

Expected result: Git reports that README.md is an untracked file.

Step 14: Stage the README

Action: Run git add README.md.

Expected result: Git stages README.md for the next commit.

Step 15: Create the first commit

Action: Run git commit -m "Initial commit".

Expected result: Git creates a commit containing the README file.

Step 16: Add the GitHub repository as a remote

Action: Run git remote add origin https://github.com/YOUR-USERNAME/my-first-project.git.

Expected result: The local repository has a remote named origin.

Step 17: Rename the branch to main

Action: Run git branch -M main.

Expected result: The current branch is named main.

Step 18: Push the commit to GitHub

Action: Run git push -u origin main.

Expected result: The main branch and its first commit are uploaded to GitHub.

Step 19: Refresh the GitHub repository

Action: Refresh the repository page in the browser.

Expected result: GitHub displays README.md and the Initial commit commit.

Screenshot Description

A screenshot should show the GitHub repository page after the successful push. It should clearly display the repository name my-first-project, the main branch, the README.md file, and the Initial commit message. This screenshot demonstrates that the local repository was successfully connected to GitHub and that the first commit was uploaded.

Troubleshooting

Common error: git is not recognized

A beginner may receive an error stating that git is not recognized as a command. This usually means Git has not been installed or the terminal cannot find the Git installation.

To fix the problem, install Git and then close and reopen the terminal. Run git --version to verify that Git is available. If the installation was successful, the command displays the installed Git version.

Exercise B: API Reference Entry
Create a New Task
Endpoint

Method: POST

Path: /api/v1/projects/{projectId}/tasks

Description

This endpoint creates a new task in a specified project.

An authenticated user must provide the project ID, task title, assignee ID, due date, and priority. A description can optionally be included.

If the task is created successfully, the API returns the newly created task and its generated task ID.

Authentication

The endpoint requires a valid bearer access token.

The token must be provided in the Authorization header using the following format:

Authorization: Bearer <access-token>

Request Headers
Header	Required	Data Type	Description
Authorization	Yes	String	Bearer token used to authenticate the user.
Content-Type	Yes	String	Must be application/json because the request body is JSON.
Accept	Yes	String	Specifies that the client expects a JSON response.
Path Parameters
Parameter	Data Type	Required	Description
projectId	String	Yes	Unique identifier of the project where the task will be created.
Request Body

The request body must be a JSON object.

Field	Data Type	Required	Description
title	String	Yes	Name or short summary of the task.
description	String	No	Additional information about the task.
assigneeId	String	Yes	Unique ID of the user assigned to the task.
dueDate	String	Yes	Date when the task is due, using YYYY-MM-DD format.
priority	String	Yes	Task priority. Allowed values are low, medium, and high.
Query Parameters

This endpoint does not use query parameters.

Example Request
POST /api/v1/projects/proj_8f31/tasks HTTP/1.1
Host: api.example.com
Authorization: Bearer eyJhbGciOi...
Content-Type: application/json
Accept: application/json

{
  "title": "Prepare project presentation",
  "description": "Create the presentation slides and prepare speaker notes.",
  "assigneeId": "usr_2048",
  "dueDate": "2026-10-15",
  "priority": "high"
}

Successful Response

Status: 201 Created

A successful response contains the newly created task.

{
  "id": "task_7c92a1",
  "projectId": "proj_8f31",
  "title": "Prepare project presentation",
  "description": "Create the presentation slides and prepare speaker notes.",
  "assigneeId": "usr_2048",
  "dueDate": "2026-10-15",
  "priority": "high",
  "status": "open",
  "createdAt": "2026-09-18T08:42:15Z"
}

HTTP Response Codes
Status Code	Meaning	When It Occurs
201 Created	Task created successfully.	The request is valid and the task has been created.
400 Bad Request	Invalid request.	The JSON is malformed or contains an invalid field value.
401 Unauthorized	Authentication failed.	The authentication header is missing, invalid, or contains an expired token.
403 Forbidden	Access denied.	The user is authenticated but does not have permission to create tasks in the project.
404 Not Found	Project not found.	The specified projectId does not identify an existing project.
409 Conflict	Request conflicts with existing data.	The request conflicts with an application or project constraint.
422 Unprocessable Entity	Validation failed.	The JSON is valid, but one or more values fail application validation, such as an invalid assigneeId.
429 Too Many Requests	Rate limit exceeded.	The client has exceeded the API request limit.
500 Internal Server Error	Server error.	An unexpected error occurs while processing the request.
503 Service Unavailable	Service unavailable.	The API is temporarily unable to process requests.
Field Validation Rules

title must be provided and must contain text.

description may be omitted.

assigneeId must identify a valid user.

dueDate must use the YYYY-MM-DD format.

priority must be exactly low, medium, or high.

projectId must identify an existing project.

The requester must have permission to create tasks in the specified project.

Summary

The POST /api/v1/projects/{projectId}/tasks endpoint allows an authenticated user to create a task within a project. The request requires a title, assignee, due date, and priority, while the description is optional. A successful request returns 201 Created together with the newly created task.

