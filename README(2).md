# Full Stack API Final Project

# Introduction

Udacity is invested in creating bonding experiences for its employees and students. A bunch of team members got the idea to hold trivia on a regular basis and created a webpage to manage the trivia app and play the game. The aim of the project was to create an API that will allow Udacity employees to play the trivia game so they can test their knowledge in a range of topics.

All backend code follows PEP8 style guidelines.

# Getting Started
Pre - requisites and Local Development

Developers using this project should already have Python3, pip and node installed on their local machines. Follow instructions to install the latest version of python for your platform in the [python docs](https://docs.python.org/3/using/unix.html#getting-and-installing-the-latest-version-of-python)

**Virtual Environment**
Ensure you have a virtual environment set up and running, this keeps your dependencies for each project separate and organised. Instructions for setting up a virtual environment for your platform can be found in the [python docs](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/).

**PIP Dependencies**
Once you have your virtual environment setup and running, install dependencies by navigating to the `/backend` directory and running:

`bash
pip install -r requirements.txt
`

This will install all of the required packages we selected within the `requirements.txt` file.

**Key Dependencies**
1. [Flask](http://flask.pocoo.org/) is a lightweight backend microservices framework. Flask is required to handle requests and responses.
2. [SQLAlchemy](https://www.sqlalchemy.org/) is the Python SQL toolkit and ORM you'll use to handle the lightweight sqlite database.
3. [Flask-CORS](https://flask-cors.readthedocs.io/en/latest/# ) is the extension we'll use to handle cross origin requests from our frontend server.

**Database Setup**
Install and setup “PostgreSQL” on the system and create a database named ‘trivia’ in the Postgres server:

`Createdb trivia`

With Postgres running, restore a database using the trivia.psql file provided. From the backend folder in terminal run:

`Cd trivia
psql trivia < trivia.psql`


**Running the server**

From within the `backend` directory, first ensure you are working using your created virtual environment.

To run the server, execute:

1. export FLASK_APP=flaskr
2. export FLASK_ENV=development
3. flask run

Setting the `FLASK_ENV` variable to `development` will detect file changes and restart the server automatically.

Setting the `FLASK_APP` variable to `flaskr` directs flask to use the `flaskr` directory and the `__init__.py` file to find the application.

**Test**
1. `dropdb trivia_test
2. createdb trivia_test
3. psql trivia_test < trivia.psql
4. python test_flaskr.py`

#API Reference

Base URL: At present this app can only be run locally and is not hosted as a base URL. The backend app is hosted at the default, http://127.0.0.1:5000/ , which is set as a proxy in the frontend configuration.

**Error Handling**

Errors are returned as JSON objects in the following format:

``({
        "success": False,
	
        "error": 404,
	
        "message": "Resource Not found"
	
    }), 404
``

The API will return two error types when requests fail:
- 404: Resources Not Found
- 422: Not Processable

**GET "/categories"**

- Returns a list of categories objects, success value and total number of categories
- Sample: ``curl http://127.0.0.1:5000/categories/``

``	{

  "categories": {
  
    "1": "Science",
    
    "2": "Art",
    
    "3": "Geography",
    
    "4": "History",
    
    "5": "Entertainment",
    
    "6": "Sports"
    
  },
  
  "success": true,
  
  "total_categories": 6
  
}
``

**GET "/questions"***
- Returns a list of questions, objects, success value and total number of  questions
- Results are paginated in groups of 10, include a request argument to choose page number, starting from 1  
- Sample: `curl http://127.0.0.1:5000/questions/?page=1`

``{
  "categories": {
    "1": "Science",
    "2": "Art",
    "3": "Geography",
    "4": "History",
    "5": "Entertainment",
    "6": "Sports"
  },
  "current_category": null,
  "questions": [
    {
      "answer": "Maya Angelou",
      "category": "4",
      "difficulty": 2,
      "id": 5,
      "question": "Whose autobiography is entitled 'I Know Why the Caged Bird Sings'?"
    },
    {
      "answer": "Muhammad Ali",
      "category": "4",
      "difficulty": 1,
      "id": 9,
      "question": "What boxer's original name is Cassius Clay?"
    },
    {
      "answer": "Apollo 13",
      "category": "5",
      "difficulty": 4,
      "id": 2,
      "question": "What movie earned Tom Hanks his third straight Oscar nomination, in 1996?"
    },
    {
      "answer": "Tom Cruise",
      "category": "5",
      "difficulty": 4,
      "id": 4,
      "question": "What actor did author Anne Rice first denounce, then praise in the role of her beloved Lestat?"
    },
    {
      "answer": "Edward Scissorhands",
      "category": "5",
      "difficulty": 3,
      "id": 6,
  "success": true,
  "total_questions": 23
}
``
**POST “/questions”**
- Creates a new question using submitted question, answer, difficulty and category, Returns the id of the created question, success value, total questions, and question list based on current page number to update the frontend
- Sample: ``curl X POST -H "Content-Type: application/json" -d '{"question": "Who won the Golden Boot at the 2018 World Cup?", "answer": "Harry Kane", "difficulty":"2", "category":"6"}' http://127.0.0.1:5000/questions/``

``{
“questions”: {
	“id” : “23”
	“question” : "Who won the Golden Boot at the 2018 World Cup?"
	“Answer”: “Harry Kane”
	"Difficulty":"2"
	"category":"6"
 	 "success": true
}
}
``

**GET “/categories/<int:category_id>/questions”**
- Returns a list of questions within a specific category
- Sample: ``curl -X GET http://127.0.0.1:5000/categories/6/questions``

``{
  "current_category": 6,
  "question": [
    {
      "answer": "Brazil",
      "category": "6",
      "difficulty": 3,
      "id": 10,
      "question": "Which is the only team to play in every soccer World Cup tournament?"
    },
    {
      "answer": "Uruguay",
      "category": "6",
      "difficulty": 4,
      "id": 11,
      "question": "Which country won the first ever soccer World Cup in 1930?"
    },
    {
      "answer": "20",
      "category": "6",
      "difficulty": 3,
      "id": 24,
      "question": "How many teams are there in the Premier League"
    },
    {
      "answer": "3",
      "category": "6",
      "difficulty": 2,
      "id": 25,
      "question": "How many Premier League cups has Arsenal won?"
    },
    {
      "answer": "Harry Kane",
      "category": "6",
      "difficulty": 2,
      "id": 26,
      "question": "Who won the Golden Boot at the 2018 World Cup?"
    },

  ],
  "success": true,
  "total_questions": 6
}
``
**DELETE ‘'/questions/<int:question_id>'**
- Deletes a question from the database,**
- Sample: ``curl -X DELETE http://127.0.0.1:5000/questions/28``

``{
  "deleted": 28,
  "success": true
}

POST “/quizzes/
Initiates the quiz, getting a list of categories, questions and enables users to submit answers
{
  "question": {
    "id": 28,
    "question": "",
    "answer": "",
    "category": 6,
    "difficulty": 2
  }
}
``
