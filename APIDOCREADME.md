## API Reference

### Trivia App

## Introduction

Udacity is invested in creating bonding experiences for its employees and students. A bunch of team members got the idea to hold trivia on a regular basis and created a webpage to manage the trivia app and play the game, but their API experience is limited and still needs to be built out.
That's where you come in! Help them finish the trivia app so they can start holding trivia and seeing who's the most knowledgeable of the bunch. The application must:

1. Display questions - both all questions and by category. Questions should show the question, category and difficulty rating by default and can show/hide the answer.
2. Delete questions.
3. Add questions and require that they include question and answer text.
4. Search for questions based on a text query string.
5. Play the quiz game, randomizing either all questions or within a specific category.

Completing this trivia app will give you the ability to structure plan, implement, and test an API - skills essential for enabling your future applications to communicate with others.

## Getting Started
   >> Base URL: At present this app can only be run locally and is not hosted as a base URL. The backend app is hosted at the default, `http://127.0.0.1:5000/`, which is set as a proxy in the frontend configuration. 
   >> Authentication: This version of the application does not require authentication or API keys. 


## Error
Errors are returned as JSON objects in the following format:

{
    "success": False, 
    "error": 400,
    "message": "bad request"
}
Response codes returned by API when requests fail include 400, 422, 404 and 500
# 404 : 
    Resource not found. 
    This occurs when the resource you are looking for does not exist.

# 422:
    Unprocessable.
    This error occurs when the request could not be processed by the server

# 400:
    Bad Request
    This error occurs when a request sent does not follow the expected request format or when a required parameter is missing from the request sent by user

# 500:
    Internal Server Error
    This error is from Trivia's app end and it occurs rarely unless the server is down or something went wrong on the server

## Endpoint Library

# Categories
    To get category resouces, this endpoint is used.
    >> Endpoint :
        GET: '/categories'
        sample request: http://localhost:5000/api/categories
        request argument: None
        response: returns object with key value pair for categories
        sample response: 
            'success': True,
            'categories' : 
                {
                    '1': "Music",
                    '2': "Art"
                }        

# Question
    >> Endpoint :
        GET /questions?page=<page_number>
        Fetches a dictionary of questions in which the keys are the answer, category, difficulty, id and question.
        request arguments: Page Number
        response: returns list of questions, number of total questions, current category and categories.

        sample Response: 
        { 
            "categories": 
            [ 
                { "id": 1, "type": "Science" },
                { "id": 2, "type": "Art" }, 
                { "id": 3, "type": "Geography" }
            ], 
            "current_category": None, 
            "questions": 
            [ 
                {"answer": "Agra", "category": 3 "difficulty": 2, "id": 15, "question": "The Taj Mahal is located in which Indian city?" }, 
                { "answer": "Escher", "category": 2, "difficulty": 1, "id": 16, "question": "Which Dutch graphic artist\u2013initials M C was a creator of optical illusions?" },
                 { "answer": "Mona Lisa", "category": 2, "difficulty": 3, "id": 17, "question": "La Giaconda is better known as what?" }, 
                 { "answer": "One", "category": 2, "difficulty": 4, "id": 18, "question": "How many paintings did Van Gogh sell in his lifetime?" }, 
                 { "answer": "Yaounde", "category": 3, "difficulty": 1, "id": 28, "question": "What is the capital of Cameroon" } 
            ], 
            "success": true, 
            "total_questions": 20 
        }

    >> Enpoint :
        DELETE /questions/<question_id>
            Delete question from the questions list.
            request arguments: question_id
            response: true if successfully deleted and returns the remaining question object 
            sample response 
            {
                "success": True,
                "deleted": question_id,
                "questions": [ 
                {"answer": "Agra", "category": 3 "difficulty": 2, "id": 15, "question": "The Taj Mahal is located in which Indian city?" }, 
                { "answer": "Escher", "category": 2, "difficulty": 1, "id": 16, "question": "Which Dutch graphic artist\u2013initials M C was a creator of optical illusions?" },
                 { "answer": "Mona Lisa", "category": 2, "difficulty": 3, "id": 17, "question": "La Giaconda is better known as what?" }, 
                 { "answer": "One", "category": 2, "difficulty": 4, "id": 18, "question": "How many paintings did Van Gogh sell in his lifetime?" }, 
                 { "answer": "Yaounde", "category": 3, "difficulty": 1, "id": 28, "question": "What is the capital of Cameroon" } 
                ], 
                "total_questions": 20,
            }

    >> Endpoint :
            POST /question/search
            Searches for the questions based on a search term
            request body: searchTerm
            sample request: {"searchTerm": "artist"}
            response: returns list of questions, number of  total questions and current category.

    >> Endpoint :
            GET /categories/<int:category_id>/questions
            To get questions based on category
            request arguments: Category Id and Page Number.
            response: returns list of questions, number of total questions, current category and categories  
            
# Quiz

    >> Endpoint :
            POST /quizzes
            To get questions to play the quiz.
            requestbody: quiz_category and previous_questions.
            response: returns random questions within the given category.

