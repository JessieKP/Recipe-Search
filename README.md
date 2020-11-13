# Write code as functions - share code frequently - try to break down big code into chunks - write notes frequently too

ask for DIETARY REQUIREMENTS:  i.e. are you vegetarian? halal?
ask for how much time they have: length of time to cook



import requests

def recipe_search(ingredient): # Register to get an APP ID and key https://developer.edamam.com/
    app_id = '9bc8ac06'
    app_key = '5c66158bf122be9926fdbd3afd09590b'
    result = requests.get(
'https://api.edamam.com/search?q={}&app_id={}&app_key={}'.format(ingredient, app_id, app_key))
    data = result.json()
    return data['hits']

def program():
    ingredient = input('What ingredient do you want to use in your cooking today? ') # Could add the spelling error message here?
    # Add extra questions here: dietary requirements, length of time to cook?
    results = recipe_search(ingredient)
    for result in results:
        recipe = result['recipe']
        print(recipe['label'])
        print(recipe['url'])
        print(recipe['healthLabels']) # This needs to change but thought was useful to see initially
        print()
        
        # Code for adding extra info (e.g. photo) or ordering the results according to calories or cooking time
        # Extension: Code offering suggestions based on what they searched? OR loop the code letting them search for more recipes?

program()
