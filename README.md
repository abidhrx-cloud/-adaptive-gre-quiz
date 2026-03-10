# Adaptive GRE Quiz System

## Overview
This project implements an adaptive GRE quiz system using Python and MongoDB. The system dynamically adjusts question difficulty based on the student's performance and generates a personalized study plan based on their weak areas.

The project demonstrates concepts from adaptive testing, Item Response Theory (IRT), and AI-assisted learning.

## Features
- GRE-style question bank stored in MongoDB
- Questions include difficulty score, topic, tags, and correct answer
- Adaptive question selection based on student ability
- Ability score updated after each response using an IRT-inspired model
- Student progress tracking through a user session
- Personalized study plan generation based on weak topics

## Technologies Used
- Python
- MongoDB Atlas
- PyMongo
- OpenAI API (for study plan generation)

## Database Structure

Database: gre_quiz

Collections:

questions
- question_text
- options
- correct_answer
- difficulty
- topic
- tags

user_sessions
- user_id
- ability_estimate
- questions_answered
- score
- total_attempts

## Adaptive Logic

1. The student starts with an initial ability score of 0.5.
2. The system selects a question whose difficulty is closest to the student's ability.
3. If the student answers correctly, the ability score increases.
4. If the student answers incorrectly, the ability score decreases.
5. The ability score is updated using a simplified Item Response Theory (IRT) approach.

IRT Formula Used:

P(correct) = 1 / (1 + e^-(ability - difficulty))

Ability Update:

new_ability = ability + learning_rate * (result - P(correct))

Where result = 1 if correct and 0 if incorrect.

## Personalized Learning Plan

After the quiz ends, the system analyzes the student's performance data:
- final ability score
- missed questions
- weak topics

This information is sent to a language model to generate a personalized 3-step study plan tailored to the student's weaknesses.

Example Output:

Personalized Study Plan

1. Review algebra fundamentals such as linear equations and exponents.
2. Practice geometry questions involving circles and triangles.
3. Take timed GRE practice tests to improve speed and accuracy.

## How to Run the Project

1. Install required libraries

pip install pymongo
pip install dnspython
pip install openai

2. Connect to MongoDB Atlas using the connection string.

3. Run the adaptive quiz script.

4. Complete the quiz to generate a personalized study plan.

## Future Improvements
- Implement full IRT models (2PL or 3PL)
- Improve question selection using better statistical methods
- Build a web interface for the quiz
- Add analytics dashboards for student performance

The system integrates an LLM through the OpenAI API to generate a personalized study plan based on the student's performance data. Due to API quota limitations, the prototype demonstrates the prompt structure and simulated output.

## Author
Syed Abid
