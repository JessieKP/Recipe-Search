import requests

# RECIPE SEARCH CODE
def recipe_search(ingredient):  # Register to get an APP ID and key https://developer.edamam.com/
    app_id = '9bc8ac06'
    app_key = '5c66158bf122be9926fdbd3afd09590b'
    result = requests.get(
        'https://api.edamam.com/search?q={}&app_id={}&app_key={}'.format(ingredient, app_id, app_key))
    data = result.json()
    return data['hits']

# PROGRAM CODE
def program():
    ingredient = input('What ingredient do you want to use in your cooking today? ')  # INGREDIENT FILTER
    # Could add the spelling error message here?
    print()
    dietary_requirements = input('List of dietary requirements we can filter results for: Vegetarian, Vegan, Nut-free, Halal, Diabetic-friendly \n Do you have a dietary requirement? (yes/no): ') # DIETARY ASSESSMENT FILTER

    correct_answers = 'yes' or 'no'

    # DIETARY FILTER REQUIRED
    if dietary_requirements == 'yes': 
        enter_dietary_requirmements = input('Enter your dietary requirement: ') # DIETARY FILTER

        correct_responses = ['vegetarian','veggie','vegan','nut-free','nut free','halal','diabetic-friendly','diabetes friendly','diabetes','diabetic']

        # VEGETARIAN FILTER
        if enter_dietary_requirmements == 'vegetarian' or 'veggie':
            results = recipe_search(ingredient)
            print()
            for result in results:
                recipe = result['recipe']

                if 'Vegetarian' in recipe['healthLabels']:
                    print(recipe['label'])
                    print(recipe['url'])
                    print()
                    
        # VEGAN FILTER
        elif enter_dietary_requirmements == 'vegan': 
                results = recipe_search(ingredient)
                print()
                for result in results:
                    recipe = result['recipe']

                    if 'Vegan' in recipe['healthLabels']:
                        print(recipe['label'])
                        print(recipe['url'])
                        print()

        # NUT-FREE FILTER
        elif enter_dietary_requirmements == 'nut-free' or 'nut free': 
                results = recipe_search(ingredient)
                print()
                for result in results:
                    recipe = result['recipe']

                    if 'Peanut-Free' or 'Tree-Nut-Free' in recipe['healthLabels']:
                        print(recipe['label'])
                        print(recipe['url'])
                        print()

        # HALAL FILTER
        elif enter_dietary_requirmements == 'halal': 
                results = recipe_search(ingredient)
                print()
                for result in results:
                    recipe = result['recipe']

                    if 'Alcohol-Free' in recipe['healthLabels'] and 'pork' not in recipe['ingredients']: # add code here
                        print(recipe['label'])
                        print(recipe['url'])
                        print()

        # DIABETIC FILTER
        elif enter_dietary_requirmements == 'diabetic-friendly' or 'diabetes friendly' or 'diabetes' or 'diabetic':
                results = recipe_search(ingredient)
                print()
                for result in results:
                    recipe = result['recipe']

                    if 'Sugar-Conscious' in recipe['healthLabels']:
                        print(recipe['label'])
                        print(recipe['url'])
                        print()
        
        # SPELLING ERROR CONTINGENCY - TRY AGAIN 
        if enter_dietary_requirmements != correct_responses:
            print('Dietary requirement submitted is not in the list. Please check spelling, refresh the program and try again.')

    # DIETARY FILTER NOT REQUIRED
    elif dietary_requirements == 'no':
        results = recipe_search(ingredient)
        print()
        for result in results:
            recipe = result['recipe']

            print(recipe['label'])
            print(recipe['url'])
            print()

    # SPELLING ERROR CONTINGENCY - LOOP THE QUESTION
    while not dietary_requirements == correct_answers:
        print('Please enter a yes or no')
        dietary_requirements = input('List of dietary requirements we can filter results for: Vegetarian, Vegan, Nut-free, Halal, Diabetic-friendly \n Do you have a dietary requirement? (yes/no): ')
        if dietary_requirements == 'yes':
            enter_dietary_requirmements = input('Enter your dietary requirement: ')

# COPY AND PASTE FINISHED DIETARY FILTER CODE

        # DIETARY FILTER NOT REQURIED - AFTER SPELLING ERROR 
        elif dietary_requirements == 'no':
            results = recipe_search(ingredient)
            print()
            for result in results:
                recipe = result['recipe']

                print(recipe['label'])
                print(recipe['url'])
                print()


# EXTENSIONS:
# Add extra questions: length of time to cook?
# Code for adding extra info (e.g. photo) or
# Code for ordering the results according to calories or cooking time
# Code offering suggestions based on what they searched? OR loop the code letting them search for more recipes?


program()


