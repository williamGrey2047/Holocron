>[!info]- Learning Outcome
>This page covers the complex nature of the multdimensional array produced by the `join` command used in Flask


# Arrays Overview

> [!info] This section provides a general overview and examples of arrays in Python and Flask. Used as background knowledge.



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

# Join Operations

**JOIN Operations for Beginners**

Imagine you have two tables in a database:

- **Customers** table with columns: `customer_id`, `name`, `email`
- **Orders** table with columns: `order_id`, `customer_id`, `product_id`, `quantity`

A JOIN operation allows you to combine rows from these two tables based on a common column, in this case `customer_id`.

There are different types of JOIN operations:

- **INNER JOIN:** Returns only rows that have matching values in both tables.

```sql
SELECT * FROM Customers INNER JOIN Orders ON Customers.customer_id = Orders.customer_id;
```

- **LEFT JOIN:** Returns all rows from the left table (Customers), and the matching rows from the right table (Orders). If there is no match in the right table, the result will be `NULL`.

```sql
SELECT * FROM Customers LEFT JOIN Orders ON Customers.customer_id = Orders.customer_id;
```

- **RIGHT JOIN:** Similar to LEFT JOIN, but returns all rows from the right table (Orders), and the matching rows from the left table (Customers).

```sql
SELECT * FROM Customers RIGHT JOIN Orders ON Customers.customer_id = Orders.customer_id;
```

- **FULL OUTER JOIN:** Returns all rows from both tables, even if there is no match.

```sql
SELECT * FROM Customers FULL OUTER JOIN Orders ON Customers.customer_id = Orders.customer_id;
```

**Using JOIN Operations in Flask**

To perform a JOIN operation in Flask, you can use the `join()` method of the `Query` object.

```python
from flask_sqlalchemy import SQLAlchemy

db = SQLAlchemy()

class Customer(db.Model):
    customer_id = db.Column(db.Integer, primary_key=True)
    name = db.Column(db.String(80))
    email = db.Column(db.String(120))

class Order(db.Model):
    order_id = db.Column(db.Integer, primary_key=True)
    customer_id = db.Column(db.Integer, db.ForeignKey('customer.customer_id'))
    product_id = db.Column(db.Integer)
    quantity = db.Column(db.Integer)

@app.route('/join')
def join():
    # Perform an INNER JOIN
    results = db.session.query(Customer, Order) \
        .join(Order, Customer.customer_id == Order.customer_id) \
        .all()

    # Process the results
    # ...

    return 'Success'
```

The `join()` method takes two arguments:

- The first argument is the table to join with.
- The second argument is the condition for joining the tables.

You can also use the `outerjoin()` method to perform LEFT, RIGHT, or FULL OUTER JOINs.

```python
# Perform a LEFT JOIN
results = db.session.query(Customer, Order) \
    .outerjoin(Order, Customer.customer_id == Order.customer_id) \
    .all()
```



# Project Specific Information

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

