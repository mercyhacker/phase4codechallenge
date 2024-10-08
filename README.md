## Flask Code Challenge - Superheroes
For this assessment, you'll be working on an API for tracking superheroes and their superpowers.


## Overview
This repository contains a Flask API for managing superheroes, their powers, and the relationships between them. You'll be tasked with completing the API's functionality as per the requirements outlined below.

## The app has the following components:

A Flask backend that powers the API.
A React frontend for testing the API.
A Postman collection for testing API endpoints.
Tests that can be run using pytest.
Contents
Setup
Models
Validations
Routes
GET /heroes
GET /heroes/
GET /powers
GET /powers/
PATCH /powers/
POST /hero_powers
## Setup
Follow these steps to set up the project:

Install dependencies for the backend and frontend:

bash
Copy code
pipenv install
pipenv shell
npm install --prefix client
Run the Flask API on localhost:5555:

bash
Copy code
python server/app.py
Run the React frontend on localhost:4000:

bash
Copy code
npm start --prefix client
Run the database migrations:

bash
Copy code
export FLASK_APP=server/app.py
flask db init
flask db upgrade head
Seed the database with initial data:

bash
Copy code
python server/seed.py
You can also test your API using Postman by importing the provided Postman collection: challenge-2-superheroes.postman_collection.json.

## Models
The API interacts with the following models:

Hero: Represents a superhero.
Power: Represents a superpower.
HeroPower: Represents the association between a hero and a power, with a strength attribute.
The relationships between these models are as follows:

A Hero has many Powers through HeroPower.
A Power has many Heroes through HeroPower.
A HeroPower belongs to a Hero and a Power.
Validations
HeroPower:

strength must be one of the following values: 'Strong', 'Weak', 'Average'.
Power:

description must be present and at least 20 characters long.
Routes
GET /heroes
Fetch a list of all heroes.

Response:

json
Copy code
[
  {
    "id": 1,
    "name": "Kamala Khan",
    "super_name": "Ms. Marvel"
  },
  {
    "id": 2,
    "name": "Doreen Green",
    "super_name": "Squirrel Girl"
  }
]
## GET /heroes/
Fetch a specific hero along with their associated powers.

## Response:

If the hero exists:

json
Copy code
{
  "id": 1,
  "name": "Kamala Khan",
  "super_name": "Ms. Marvel",
  "hero_powers": [
    {
      "hero_id": 1,
      "id": 1,
      "power": {
        "description": "gives the wielder the ability to fly",
        "id": 2,
        "name": "flight"
      },
      "power_id": 2,
      "strength": "Strong"
    }
  ]
}
## If the hero does not exist:

json
Copy code
{
  "error": "Hero not found"
}
GET /powers
Fetch a list of all powers.

## Response:

json
Copy code
[
  {
    "description": "gives the wielder super-human strengths",
    "id": 1,
    "name": "super strength"
  },
  {
    "description": "gives the wielder the ability to fly",
    "id": 2,
    "name": "flight"
  }
]
## GET /powers/
Fetch a specific power.

Response:

If the power exists:

json
Copy code
{
  "description": "gives the wielder super-human strengths",
  "id": 1,
  "name": "super strength"
}
If the power does not exist:

json
Copy code
{
  "error": "Power not found"
}
## PATCH /powers/
Update an existing power's description.

Request Body:

json
Copy code
{
  "description": "Valid Updated Description"
}
## Response:

If the power is updated successfully:

json
Copy code
{
  "description": "Valid Updated Description",
  "id": 1,
  "name": "super strength"
}
If the power does not exist:

json
Copy code
{
  "error": "Power not found"
}
If the validation fails:

json
Copy code
{
  "errors": ["validation errors"]
}
POST /hero_powers
Assign a power to a hero.

## Request Body:

json
Copy code
{
  "strength": "Average",
  "power_id": 1,
  "hero_id": 3
}
## Response:

If the HeroPower is created successfully:

json
Copy code
{
  "id": 11,
  "hero_id": 3,
  "power_id": 1,
  "strength": "Average",
  "hero": {
    "id": 3,
    "name": "Gwen Stacy",
    "super_name": "Spider-Gwen"
  },
  "power": {
    "description": "gives the wielder super-human strengths",
    "id": 1,
    "name": "super strength"
  }
}
If the validation fails:

json
Copy code
{
  "errors": ["validation errors"]
}
## author 
mercy mumbua
## git hub
https://github.com/mercyhacker