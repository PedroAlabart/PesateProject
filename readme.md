
# Pesate  ![hola](static/Logo-png3.png)
Pesate documents recipes and displays the cost of their ingredients in both Argentine pesos and US dollars.

## Table of Contents

- [About](#about)
- [Demo](#demo) 
- [Getting Started](#getting_started)
- [Usage](#usage)
- [Files](#files)

## About
The purpose of this application is to document recipes and display the cost of their ingredients in both Argentine pesos and US dollars.


My goal is to help people who sell pastry recipes generate extra income by using a tool that will help them manage their budget.



## Demo

See my demo in youtube with this [link](https://youtu.be/9vpQ5jjcg7Q).

## Getting Started
1. Clone it from github
2. In the command line:
        pip install -r requirements.txt 
3. In the command line :
    cd Pagina
    py -m flask run 

## Usage
There are 4 different pages in the app, as you can see in the navigation bar:
    ![Navbar](static/NavBar.png)


 ### Calculadora
 * **English:** Calculator.
 * Calculates the cost of ingredients for a selected recipe.
 * Allows the user to input the quantity of times they want to cook the recipe, and calculates the total cost accordingly.




### Agregar recetas
* **English:** Add recipe.
* Adds a new recipe to the database.
* Offers a list of 30 ingredients to choose from.






### Borrar recetas
 * **English:** Delete recipe.
* Removes a recipe from the database.


### Precios
* **English:** Prices
*Shows a table with the following columns:
    *Name: Ingredient name.
    *Price: Price per kg/liter or unit (for eggs).
    *Link: Link to the supermarket page.


## Files

### Py files
#### Database
* Created with SQLAlchemy. 
* agregar_ingrediente: Adds an ingredient to the table
* producto_precio:  Web-scrapes the price of a product given its name and URL. Returns a dictionary with the product as the key and the price as the value.
* updatear_precio: Calls all the above functions by first calling producto_precio for web-scraping, then adding the price to the table with agregar_ingrediente.
buscar_ingrediente: Returns the price per kg/lt/unit. This function is used on the home tab when you select an ingredient
#### Dblue
*Uses the DolarSi API to get the selling value for the Dollar Blue.

#### MercadoPago
* Shows the ingredient list in a dictionary with the keys being the product and the values the URL to webscrap
* The list of ingredients is pre-defined, covering most pastry recipe ingredients.
* There is a limitation to which products are on the Dia Page, for example the cocoa powder had to be web-scrapped from another market



#### Webforms
In all webforms i had the problem of having to update the choices of recipes. I had a rare "bug", the recipes only updated when i saved the .py file, i spent days trying to figure out how to make the user to save a file
The solution was actually very simple, with an __init__ function the choices update automatically

### HTML Templates

#### Recetas
* I decided to use a select form for the ingredients for my limitation of not knowing how to have a list of user-inputs 

### Precios
* Two tables are used in the "Prices" feature to minimize scrolling for the 30 ingredients.


Thanks for reading!




