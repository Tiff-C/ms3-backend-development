# NomNoms

   This project is my third Milestone Project, the purpose of this project is to demonstrate the skills and knowledge I have developed during the Python Essentials and Backend Development modules. I have chosen project idea 1 - create an online cookbook.

## About the project

   - This web application will be built using [Python](https://www.python.org/), [Flask](https://flask.palletsprojects.com/en/2.0.x/), [MongoDB](https://www.mongodb.com/), and a frontend framework called [Materialize](https://materializecss.com/).  
   - It  will allow users to store and easily access recipies via CRUD calls to a Mongo database.
   - This will be done in the context of a Flask application with HTML based user interfaces.

### Design

- __External Users Goal__: Find and share recipies.
- __Site Owner's Goal__: Promote a brand of cooking tools.

### Database Schema

When thinking about my databases structure I decided to see if I could find any example recipie database's. During my search I found [schema.org/Recipe](https://schema.org/Recipe) and the specific [Schema](https://developers.google.com/search/docs/advanced/structured-data/recipe) Google use for their recipies database. Using these and [The Meal DB](https://www.themealdb.com/) for catagories and cuisine lists, I decided on the following structure for my database.

__Collections:__ 
1. Users

   The user authentication for this project will reuse the code from the [Mini Project Walkthrough](https://github.com/Tiff-C/task-master) with the addition of `superusers` to authenticate admin users instead of `if username.lower() == 'admin'`.

   ```JSON
   {
      "username": "username",
      "password": "password"
   }
   ```

2. Categories

   The categories list has been taken from [The Meal DB | Categories](https://www.themealdb.com/api/json/v1/1/list.php?c=list). The categories will be available for users to select when inputting a recipe. I have decided on the use of the categories TheMealDb to avoid the creation of duplicate categories through typo errors, naming variations etc. Adding and removing categories will require `superuser` to be set to `True`.

   ```JSON
   {
      "recipeCategory": "category"
   }
   ```

3. Cuisines

   The cuisines list has been taken from [The Meal DB | Cuisines](www.themealdb.com/api/json/v1/1/list.php?a=list). The cuisines will be available for users to select when inputting a recipe.  I have decided on the use of the cuisines used by TheMealDb to avoid the creation of duplicate cuisines through typo errors, naming variations etc. Adding and removing categories will require `superuser` to be set to `True`.

   ```JSON
   {
      "recipeCuisine": "cuisine"
   }
   ```

4. Recipes

   For my recipies collection I will be using a condensed version of the [Recipes Schema](https://schema.org/Recipe) from [Schema.org](https://schema.org/). An example of this and the expected data types can be seen below. 
   This format along with the flexibility providided by using a non-relational database like MongoDB will allow users to add their own units and measurements based on preference. I could add all units and measurements that users can then select as I have for Categories however due to the large variation of units and measurements used in recipies (e.g 'a pinch of salt', 'a slice of bread', 'half a pack of biscuits')I have decided that for now it would be best to let users input this themselves. This is something I may look at in the future to bring a little more uniformity to my data however I feel this is not required for my milestone project.

   ```JSON
   {
      "name": "text",
      "prepTime": "duration",
      "cookTime": "duration",
      "cookingMethod": "text",
      "recipeCategory": "text",
      "recipeCuisine": "text",
      "recipeIngredient": ["item list"],
      "recipeInstructions": ["item list"],
      "recipeYield": "quantative value",
      "recipeImage": "url",
      "tools": ["item list"]
   }
   ```