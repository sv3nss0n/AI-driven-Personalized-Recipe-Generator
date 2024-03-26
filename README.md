# AI-driven-Personalized-Recipe-Generator
利用机器学习根据用户的口味、饮食限制和可用食材生成个性化食谱。
import random

# Mock database of recipes
recipes_db = [
    {"name": "Spaghetti Carbonara", "ingredients": ["pasta", "eggs", "cheese", "bacon"], "diet": ["vegetarian"]},
    {"name": "Vegan Tacos", "ingredients": ["tortillas", "black beans", "avocado", "tomato", "lettuce"], "diet": ["vegan", "vegetarian"]},
    {"name": "Chicken Curry", "ingredients": ["chicken", "rice", "curry powder", "coconut milk"], "diet": []},
    # Add more recipes
]

# Mock ML model for predicting user taste preferences
class TastePreferenceModel:
    def predict(self, user_preferences):
        # In a real scenario, use a trained model to predict and return preferred recipes.
        # This is just a placeholder returning random preferences.
        return random.choice(["vegetarian", "vegan", ""])

def filter_by_dietary_restrictions(recipes, dietary_restrictions):
    if not dietary_restrictions:
        return recipes
    return [recipe for recipe in recipes if set(dietary_restrictions).issubset(recipe["diet"])]

def filter_by_available_ingredients(recipes, available_ingredients):
    return [recipe for recipe in recipes if all(item in available_ingredients for item in recipe["ingredients"])]

def generate_personalized_recipe(user_preferences, dietary_restrictions, available_ingredients):
    model = TastePreferenceModel()
    preferred_diet = model.predict(user_preferences)
    
    if preferred_diet:
        dietary_restrictions.append(preferred_diet)
    
    filtered_recipes = filter_by_dietary_restrictions(recipes_db, dietary_restrictions)
    final_recipes = filter_by_available_ingredients(filtered_recipes, available_ingredients)
    
    if final_recipes:
        return random.choice(final_recipes)  # Randomly select one of the matching recipes
    else:
        return "No matching recipes found based on your preferences and available ingredients."

# Example usage
user_preferences = {"likes_spicy": True, "prefers_vegetarian": False}
dietary_restrictions = ["vegetarian"]
available_ingredients = ["pasta", "eggs", "cheese", "bacon"]

print(generate_personalized_recipe(user_preferences, dietary_restrictions, available_ingredients))
