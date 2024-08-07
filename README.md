# a-balanced-daily-diet-for-middle-aged-women
# app.py
from flask import Flask, request, render_template
import random

app = Flask(__name__)

# Example food items with their nutritional content (calories, protein, fat, carbs)
FOOD_ITEMS = [
    {"name": "Chicken Breast", "calories": 165, "protein": 31, "fat": 3.6, "carbs": 0},
    {"name": "Broccoli", "calories": 55, "protein": 3.7, "fat": 0.6, "carbs": 11},
    {"name": "Almonds", "calories": 575, "protein": 21, "fat": 49, "carbs": 22},
    {"name": "Oatmeal", "calories": 150, "protein": 5, "fat": 3, "carbs": 27},
    {"name": "Salmon", "calories": 208, "protein": 20, "fat": 13, "carbs": 0},
    {"name": "Apple", "calories": 95, "protein": 0.5, "fat": 0.3, "carbs": 25},
]

# Example nutritional requirements for middle-aged women
DAILY_REQUIREMENTS = {
    "calories": 2000,
    "protein": 46,  # in grams
    "fat": 70,  # in grams
    "carbs": 250,  # in grams
}

def generate_meal_plan():
    meal_plan = []
    total_nutrition = {"calories": 0, "protein": 0, "fat": 0, "carbs": 0}

    while total_nutrition["calories"] < DAILY_REQUIREMENTS["calories"]:
        food_item = random.choice(FOOD_ITEMS)
        meal_plan.append(food_item)

        for nutrient in total_nutrition:
            total_nutrition[nutrient] += food_item[nutrient]

        if len(meal_plan) > 20:  # Prevent infinite loop
            break

    return meal_plan, total_nutrition

@app.route('/')
def index():
    return render_template('index.html')

@app.route('/generate', methods=['POST'])
def generate():
    meal_plan, total_nutrition = generate_meal_plan()
    return render_template('meal_plan.html', meal_plan=meal_plan, total_nutrition=total_nutrition)

if __name__ == '__main__':
    app.run(debug=True)
<!DOCTYPE html>
<html>
<head>
    <title>Balanced Daily Diet</title>
</head>
<body>
    <h1>Balanced Daily Diet for Middle-Aged Women</h1>
    <form action="/generate" method="post">
        <button type="submit">Generate Meal Plan</button>
    </form>
</body>
</html>
<!DOCTYPE html>
<html>
<head>
    <title>Your Meal Plan</title>
</head>
<body>
    <h1>Your Balanced Daily Meal Plan</h1>
    <ul>
        {% for item in meal_plan %}
            <li>{{ item.name }} - Calories: {{ item.calories }}, Protein: {{ item.protein }}g, Fat: {{ item.fat }}g, Carbs: {{ item.carbs }}g</li>
        {% endfor %}
    </ul>
    <h2>Total Nutrition</h2>
    <p>Calories: {{ total_nutrition.calories }}</p>
    <p>Protein: {{ total_nutrition.protein }}g</p>
    <p>Fat: {{ total_nutrition.fat }}g</p>
    <p>Carbs: {{ total_nutrition.carbs }}g</p>
</body>
</html>

Creating a balanced daily diet application involves several steps, including defining the nutritional requirements for middle-aged women, generating meal plans, and ensuring the diet meets these requirements. The application will include a backend to handle the logic and a simple front end to interact with the user.

Here's an outline of the necessary code, including a simple frontend and backend using Python (Flask for the backend and HTML/CSS for the frontend):

Running the Application.
1 Save the backend code to a file named app.py.
2 Create a directory named templates in the same directory as app.py.
3 Save index.html and meal_plan.html inside the templates directory.
4 Install Flask if you haven't already by running pip install Flask.
5 Run the Flask application by executing python app.py.
This application will generate a simple balanced daily meal plan based on predefined nutritional requirements for middle-aged women. You can expand the FOOD_ITEMS list and improve the logic for generating meal plans to make it more robust and tailored to individual preferences and dietary restrictions.
