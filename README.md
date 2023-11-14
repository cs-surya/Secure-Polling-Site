Overview
Welcome to the Secure Polling Site, a secure and interactive platform for creating and participating in polls. This documentation provides a basic schema and overview of both the backend and frontend components.

Backend
Technologies Used
Framework: Microsoft.AspNetCore.Mvc
Authentication: JSON Web Token (JWT)
Database: Entity Framework Core with SQL Server
Security: Passwords hashed using SHA256
Authorization: Admin and user roles
Database Schema
User

UserID (int, primary key)
Username (string, required, unique)
PasswordHash (string, required)
IsAdmin (bool, default: false)
Poll

PollID (int, primary key)
Question (string, required)
IsActive (bool, default: false)
WinnerOption (string)
Option1 (string, required)
Option2 (string, required)
AllowedUserIds (collection of int)
Vote

VoteID (int, primary key)
UserID (int, foreign key to User)
PollID (int, foreign key to Poll)
VotedOption (string, required)
API Endpoints
User Registration

Endpoint: POST /api/users/register
Request Body: { "Username": "string", "PasswordHash": "string", "IsAdmin": "bool" }
User Login

Endpoint: POST /api/users/login
Request Body: { "Username": "string", "PasswordHash": "string" }
Response: { "Message": "string", "Token": "string", "IsAdmin": "bool" }
Create Poll

Endpoint: POST /api/polls/create
Request Body: { "Question": "string", "Option1": "string", "Option2": "string", "AllowedUserIds": [int] }
Get Current Poll

Endpoint: GET /api/polls/current
Response: Poll object or "No active poll"
Submit Vote

Endpoint: POST /api/polls/submit
Request Body: { "UserID": "int", "PollID": "int", "VotedOption": "string" }
Response: "Vote submitted successfully" or error message
End Poll

Endpoint: POST /api/polls/end
Request Body: { "PollID": "int" }
Response: "Poll ended successfully. Winner: [Option]" or error message
Frontend
User Registration (register.html)
HTML form with fields for username, password, and admin checkbox.
JavaScript function (registerUser()) to send registration data to the backend.
User Login (login.html)
HTML form with fields for username and password.
JavaScript function (loginUser()) to send login data to the backend and handle the response.
Poll Page (poll.html)
Display the current active poll.
HTML form (voteForm) with a dropdown for selecting an option.
JavaScript functions to fetch and display the current poll (getCurrentPoll()) and submit a vote (submitVote()).
Admin Page (admin.html)
HTML form (createPollForm) for creating a new poll.
Display current users and allowed users.
JavaScript functions to fetch current users (getCurrentUsers()), create a poll (createPoll()), end the current poll, and display the winner (endCurrentPoll(), displayWinner()).
How to Run
Open each HTML file in a web browser.
Ensure the backend is running at http://localhost:5160.
Interact with the respective pages.
Conclusion
This basic schema provides a foundation for further development of the Secure Polling Site. 
