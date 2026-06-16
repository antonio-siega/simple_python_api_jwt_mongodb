# Python API with JWT and MongoDB
Simple Python API with JWT-based authentication and persistent cloud storage using MongoDB. Done as a project for the "Web API Development" subject during my 5th semester in the Information Systems course (Bachelor's Degree).

## Requirements
* Python >= 3.13
* Flask >= 3.1.1
* Werzkeug >= 3.1.3
* Pymongo >= 4.17.0

## Usage
Insert your MongoDB connection string in the MongoClient object initialization (inside ```main.py```). Then, go into your MongoDB Atlas Project dashboard and authorize your current IP for connections. Run ```main.py``` and send requests to the endpoints of http://localhost:5000/ listed below. The port can be easily changed in the source code at your discretion. To access JWT-authenticated endpoints, you must first register through the POST /register endpoint and then get the access token from the POST /login endpoint.

## Unauthenticated Endpoints
### POST /register
For user registration. Receives a POST request with a JSON format body. Fields are specified below:
```
{
  "id": INT (required, unique),
  "username": STRING (required),
  "email": STRING (required, unique),
  "password": STRING (required)
}
```
### POST /login
For user authentication, provides a JWT in response. Receives a POST request with a JSON format body. Fields are specified below:
```
{
  "email": STRING (required),
  "password": STRING (required)
}
```

## Authenticated Endpoints
All endpoints from here on require an "Authorization" header formatted as follows: "Bearer {JWT}" (without the curly braces).
### POST /tasks
Creates a task associated to the current user. Fields are specified below:
```
{
  "id": INT (required, unique),
  "title": STRING (required),
  "description": STRING (optional),
  "status": STRING (required)
}
```
### GET /tasks
Lists all tasks associated to the current user.
### GET /tasks/<int:id>
Lists the task associated with the specified id if it belongs to the current user.
### PUT /tasks/<int:id>
Updates the task associated with the specified id if it belongs to the current user. All fields specified in the POST /tasks section can be updated except for "id".
### DELETE /tasks/<int:id>
Deletes the task associated with the specified id if it belongs to the current user.
