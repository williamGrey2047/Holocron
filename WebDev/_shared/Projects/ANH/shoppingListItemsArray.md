>[!info]- Learning Outcome
>This page covers the complex nature of the multdimensional array produced by the `join` command used in Flask

# Background

In the Shopping List stage of the project, to display a shopping list to the user, including the items in the list and the item names, data needs to be retrieved from two different tables at the same time

The database, focusing on the shopping list sub-system, is visualised in the Entity Relationship Diagram (ERD) as:

![erdShoppingLists](/WebDev/_shared/Projects/ANH/images/erdShoppingLists.png)

This diagram describes:
- `shopping_lists` is linked to the `User` table through the `userID`->`id` fields connection.
- `shopping_list_items` link individual `shopping_item` entries to individual `shopping_lists`. 

**In summary:** To display an individual shopping list to the user, the list of items needs to be retrieved from `shopping_list_items` and each item's name needs to be retrieved from `shopping_item`. This requires a `join` operation on the database.

## Sample Data

Using the information above, and the sample data below, you can see that in the shopping_list_items table, the record with an ID of 4 matches the `shoppingListID` of 2 with the item with an ID of 5, named "Self Raising Flour" from the `shopping_item` table.

### `shopping_item`

| id    | name               |
| ----- | ------------------ |
| 1 | Taco               |
| 2 | Cheese             |
| 3 | Bread              |
| 4 | Flour              |
| 5 | Self Raising Flour |
| 6 | d                  |
| 7 | 3                  |
| 8 | ads                |

### `shopping_list_items`

| id    | shoppingListID | shoppingItemID | quantity | completed |
| ----- | -------------- | -------------- | -------- | --------- |
| 4 | 2          | 5          | 10   | 0     |
| 5 | 1              | 6              | d        | 1         |




# Arrays Overview

## Arrays and Multidimensional Arrays in Python and Flask

### Single-Dimensional Arrays

**Python**

Single-dimensional arrays in Python are simply lists. You can create a single-dimensional array using square brackets `[]`.

```python
fruits = ["apple", "banana", "cherry"]
```

You can access elements in the array using their index.

```python
print(fruits[0])  # Output: apple
```

You can also iterate over the array using a `for` loop.

```python
for fruit in fruits:
    print(fruit)
```

**Flask**

Flask provides a way to handle single-dimensional arrays as part of HTTP requests and responses. To receive a single-dimensional array from a client, you can use the `request.json` object.

```python
from flask import Flask, request

app = Flask(__name__)

@app.route('/array', methods=['POST'])
def receive_array():
    # Get the array from the request body
    array = request.json.get('array')

    # Process the array
    # ...

    return 'Success'
```

To send a single-dimensional array to a client, you can use the `jsonify()` function.

```python
from flask import Flask, jsonify

app = Flask(__name__)

@app.route('/array', methods=['GET'])
def send_array():
    # Create a single-dimensional array
    array = ["apple", "banana", "cherry"]

    # Send the array to the client
    return jsonify(array)
```

### Multidimensional Arrays

**Python**

Multidimensional arrays in Python are represented using nested lists. You can create a multidimensional array using square brackets `[]` and nested square brackets `[][]`.

```python
board = [['X', '.', '.'],
         ['.', 'O', '.'],
         ['.', '.', 'X']]
```

You can access elements in the array using their indices.

```python
print(board[0][0])  # Output: X
```

You can also iterate over the array using nested `for` loops.

```python
for row in board:
    for cell in row:
        print(cell)
```

**Flask**

Flask provides a way to handle multidimensional arrays as part of HTTP requests and responses. To receive a multidimensional array from a client, you can use the `request.json` object.

```python
from flask import Flask, request

app = Flask(__name__)

@app.route('/multi_array', methods=['POST'])
def receive_multi_array():
    # Get the multidimensional array from the request body
    array = request.json.get('array')

    # Process the array
    # ...

    return 'Success'
```

To send a multidimensional array to a client, you can use the `jsonify()` function.

```python
from flask import Flask, jsonify

app = Flask(__name__)

@app.route('/multi_array', methods=['GET'])
def send_multi_array():
    # Create a multidimensional array
    array = [['X', '.', '.'],
             ['.', 'O', '.'],
             ['.', '.', 'X']]

    # Send the array to the client
    return jsonify(array)
```

