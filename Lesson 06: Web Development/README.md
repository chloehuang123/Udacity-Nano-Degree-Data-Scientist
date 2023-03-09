# Lesson 06: Web Development

### Creating New Pages
To create a new web page, you first need to specify the route in the routes.py as well as the name of the html template.
```
@app.route('/new-route')
def render_the_route():
    return render_template('new_route.html')
```
The route name, function name, and template name do not have to match; however, it's good practice to make them similar so that the code is easier to follow.

The new_route.html file must go in the templates folder. Flask automatically looks for html files in the templates folder.

### What is @app.route?
To use Flask, you don't necessarily need to know what @app.route is doing. You only have to remember that the path you place inside of @app.route() will be the web address. And then the function you write below @app.route is used to render the correct html template file for the web address.

In Python, the @ symbol is used for decorators. Decorators are a shorthand way to input a function into another function. Take a look at this code. Python allows you to use a function as an input to another function:
```
def decorator(input_function):

    return input_function

def input_function():
    print("I am an input function")

decorator_example = decorator(input_function)
decorator_example()
```
This code will print out:

Decorator function

I am an input function

Instead of using a decorator function, you could get the same behavior with the following code:
```
input_function = decorator(input_function)
input_function()
```
Because @app.route() has the . symbol, there's an implication that app is a class (or an instance of a class) and route is a method of that class. Hence a function written underneath @app.route() is going to get passed into the route method. The purpose of @app.route() is to make sure the correct web address gets associated with the correct html template. This code
```
@app.route('/homepage')
def some_function()
  return render_template('index.html')
```
is ensuring that the web address 'www.website.com/homepage` is associated with the index.html template.

If you'd like to know more details about decorators and how @app.route() works, check out these tutorials:

[how @app.route works](https://ains.co/blog/things-which-arent-magic-flask-part-1.html)

[general decorators tutorial](https://realpython.com/primer-on-python-decorators/)
