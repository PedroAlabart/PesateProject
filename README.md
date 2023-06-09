
# Pesate  ![hola](Pagina/static/Logo-png3.png)

### Pesate documents recipes and displays the cost of their ingredients in both Argentine pesos and US dollars.

The project took me 20 days and I had to use the following technologies:

* *SQLAlchemy* to store ingredients. I used a relational table because I wanted all ingredients to have a name, price, and purchase link.
* I had to refresh my knowledge of *JavaScript* in order to create functions that enable the addition or removal of ingredients from a recipe
* *JSON* to store recipes. Due to the variability of recipes, I felt that a non-relational database was the best way to store them.
 
* *Flask,  Jinja* help for building web applications
* *Bootstrap* to help in the styling and responsivness of the page 


![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)<space><space>![JavaScript](https://img.shields.io/badge/javascript-%23323330.svg?style=for-the-badge&logo=javascript&logoColor=%23F7DF1E)<space><space>![Flask](https://img.shields.io/badge/flask-%23000.svg?style=for-the-badge&logo=flask&logoColor=white)![Bootstrap](https://img.shields.io/badge/bootstrap-%23563D7C.svg?style=for-the-badge&logo=bootstrap&logoColor=white)
***

## Table of Contents

- [About](#about)
- [Demo](#demo) 
- [Getting Started](#getting_started)
- [Usage](#usage)
- [Files](#files)
- [Issues](#issues)

***

## About
By using the "Pesate" application, users can easily calculate the cost of ingredients, store recipes, and view the updated prices of ingredients in both Argentine pesos and US dollars.


The purpose of this application is to help people who sell pastry recipes generate extra income by using a tool that will help them manage their budget.

This tool is  useful for anyone in Argentina who loves baking and wants to keep track of their expenses. 

The price of the products in Pesos is webscrapped from the page of [Supermercados Dia](https://diaonline.supermercadosdia.com.ar/?gad=1&gclid=CjwKCAjwov6hBhBsEiwAvrvN6NS0ZnDmQilgYjsKAb0UYmBX2N6nWiIsBG7AIFovtPaoPyRUnCpXtBoCRdYQAvD_BwE&gclsrc=aw.ds).
The [DolarSi](https://www.dolarsi.com/) API facilitates the extraction of the selling price value of the 'blue dollar' 

My goal is to help people who sell pastry recipes generate extra income by using a tool that will help them manage their budget.


***

## Demo

The first half of the video features a PowerPoint presentation where I introduce the purpose and design of the page.
In the second half, I switch to a screen recording of myself navigating through the actual page and demonstrating its features.
[Watch it here!](https://youtu.be/9vpQ5jjcg7Q)

***

## Getting Started
1. Go to the GitHub repository and click on the "Clone or download" button.
2. Open your terminal and navigate to the directory where you want to clone the project.
3. Create a virtual environment by running the command
    ```
    py -m virtualenv venv
    ```

4. Activate the virtual environment by running the command
    ```
    venv/bin/activate
    ```
    or
    ```
    venv/Scripts/activate
    ```
5. Run the command to install the needed packages
    ```
    pip install -r requirements.txt 
    ```

6. In the command line :
    ```
    cd Pagina
    py -m flask run
    ```
7. The application should start running, and you can access it by opening a web browser and navigating to http://localhost:5000/.
***
## Usage
There are 4 different pages in the app, as you can see in the navigation bar:
    ![Navbar](Pagina/static/NavBar.png)


 ### Calculadora
 * **English:** Calculator.
 * This is the home page, which is the default landing page when the user opens the app, it shows the first recipe in the dictionary 
 * Calculates the cost of ingredients for a selected recipe.
 * Allows the user to input the quantity of times they want to cook the recipe, and calculates the total cost accordingly.
 * Provides a convenient way to estimate the cost of ingredients for any given recipe.

    ![Navbar](Pagina/static/Calculadora.png)


***
### Agregar recetas
* **English:** Add recipe.
* Adds a new recipe to the database.
* Offers a list of 30 ingredients to choose from.
* Shows a green flash to show that the recipe was correctly added.
* Provides an easy way to expand the recipe database with new recipes.

    ![Agregar](Pagina/static/Agregar.png)





***
### Borrar recetas
 * **English:** Delete recipe.
* Removes a recipe from the database.
* Shows a red flash to indicate which recipe was deleted.
* Provides a simple way to manage the recipe database and remove any unwanted recipes.

    ![Borrar](Pagina/static/Borrar.png)


***
### Precios
* **English:** Prices
* Shows a table with the following columns:
    * Name: Ingredient name.
    * Price: Price per kg/liter or unit (for eggs). Both in Pesos and Dollars
    * Link: Link to the supermarket page.
* The button "Actualizar Precios" calls the "updatear_precio" function, explained down below. This event takes from 40 seconds to 1 minute

    ![Precios](Pagina/static/Precios.png)


## Files

### Recetario.JSON
* The best way to store such a diverse range of recipes is by using a JSON file.
* A key-value system was implemented for each recipe, where the keys represent the name of the recipe, and the values of each key represent the ingredients required for that recipe, which are also stored as key-value pairs.

```
"Brownie Nadia": {"Chocolate": "150", "Manteca": "100", "Huevos": "2", "Az\u00facar": "150", "Harina Leudante": "75"},
"Pochoclos": {"Maiz Pisingallo": "108", "Az\u00facar": "135"}
```


### Py files

#### Helper functions in APP.py

The helper functions are :
* Usd
* Pesos
##### Pesos:
* Displays the number with a the $ sign and  no decimals.
* I don't use decimals for pesos because cents are insignificant in a purchase
* There are some ingredients, such as salt, that are used like 5 grams per recipe. This amount gives a value in pesos that is less than 1, and in these cases, the function rounds up to 1.
* Example: 15.5 = $15  

##### Usd:
* Displays the number with a the USD sign and 2 decimals.
* Dollars have a number
* Example: 15.5 = $15,5  

#### Database.py
* Created with SQLAlchemy.
* In the database, there is a table named "Ingredientes" with the following columns: ingredient name as a string, ingredient price as an integer, and purchase link as a string.
* I decided to save the link so that the user can check in the prices page which product i selected. For example, flour has three very popular brands,  I wanted the user to be able see which brand I personally chose as the one that is saved in the database.





* Database.py contains 4 functions: 
    * *agregar_ingrediente:* Adds an ingredient to the table
    * *producto_precio:*  Web-scrapes the price of a product given its name and URL. Returns a dictionary with the product as the key and the price as the value.
    * *updatear_precio:* Calls all the above functions by first calling producto_precio for web-scraping, then adding the price to the table with agregar_ingrediente.
    *buscar_ingrediente:* Querys for the ingredient name and returns the price per kg/lt/unit. This function is used on the home tab when you select an ingredient

#### Dblue.py
* The DolarSi API provides a simple and easy-to-use interface for retrieving the current exchange rates for various currencies in Argentina, including the selling value for the Dollar Blue.
* I used the requests library to make the API request and the json library to parse the JSON response. 

#### MercadoPago.py
* Shows the ingredient list in a dictionary with the keys being the product and the values the URL to webscrap
* The list of ingredients is pre-defined, covering most pastry recipe ingredients.
* There is a limitation to which products are on the Dia Page, for example the cocoa powder had to be web-scrapped from another market



#### Webforms
In all webforms i had the problem of having to update the choices of recipes. I had a rare "bug", the recipes only updated when i saved the .py file, i spent days trying to figure out how to make it so the user can save the .py file
The solution was actually very simple, with an __init__ function the choices update automatically 


### HTML Templates

### Calculadora
* The form will autosubmit when a recipe is selected or when the user presses enter or clicks outside the integer field.
* Upon opening the page, the form will display the table with the first item in the 'recetario.json' file. In the previous version, the page appeared empty until a recipe was clicked. This change was made to help users better understand the concept of the form.

#### Agregar recetas
* This is the section  page i made. It took me the most time because i had to learn about WTForm and Json.
* I decided to use a select form for the ingredients for my limitation of not knowing how to have a list of user-inputs, and because i can only output the price of the products in the Dia shop
* My first take to select multiple ingredients was using a FieldList but they don't work as expected and discovered that a simple fieldlist was enough.
* The "add ingredient" button was made with javascript, i couldn't understand how to use jinja and js in different files so i used an script tag at the end of the html. 
* The X button to delete ingredients is on a different file because it didn't need to use jinja and wtform.

### Precios
* Two tables are used in the "Prices" feature to minimize scrolling for the 30 ingredients.
* When i made this section i had 29 ingredients. Bootstrap made 2 tables, one with 15 ingredients and another with 14, but the second one had a problem, it had different a row height. To fix this i added if statment so that if the ingredients where an odd number the second table would get an empty row, this change made the tables the same height.
* But when i added the 30rd ingredient, the tables broke again so i scrapped the idea, deleted the if statement and let it be with an even number of 30 ingredients. 


## Issues
* The testing was incomplete, as it did not cover scenarios such as the deletion of all recipes or the saving of an empty recipe, leaving uncertainties about the application's behavior in such situations.
* In the prices section of the app, the user is required to update the prices manually. This decision was made to prioritize efficiency as automatic updates were found to take approximately 70 seconds to complete. By allowing users to update the prices manually, they are given the flexibility to decide when to initiate the update process, thereby optimizing their experience with the app.
* At the moment, there is no specific section on the app to directly edit a recipe. This means that if you want to make any changes to a recipe, you will have to delete the existing one and add it again with the updated information. While this process can be a bit time-consuming and inconvenient, it is currently the only way to make any modifications to a recipe that has already been added to the app.
* If you add a recipe with the same name as one already saved, the latter will be overwritten instead of asking you to choose another name.

The current state of the page is functional for my needs, however, I will continue to try to address the listed issues over time.

Thanks for reading! <3
Pesate.





