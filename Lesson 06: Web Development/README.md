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

### Summary Part 1
The purpose of this section is to give you an idea of how the final web app works in terms of passing information back and forth between the back end and front end. The web template you'll be using at the end of the lesson will already provide the code for sharing information between the back and front ends. Your task will be to wrangle data and set up the plotly visualizations using Python. But it's important to get a sense for how the web app works.

In the video above, the data set was sent from the back end to the front end. This was accomplished by including a variable in the render_template() function like so:
```
data = data_wrangling()

@app.route('/')
@app.route('/index')
def index():
   return render_template('index.html', data_set = data)
```
What this code does is to first load the data using the data_wrangling function from wrangling.py. This data gets stored in a variable called data.

In render_template, that data is sent to the front end via a variable called data_set. Now the data is available to the front_end in the data_set variable.

In the index.html file, you can access the data_set variable using the following syntax:
```
{{ data_set }}
```
You can do this because Flask comes with a template engine called Jinja. Jinja also allows you to put control flow statements in your html using the following syntax:
```
{% for tuple in data_set %}
  <p>{{tuple}}</p>
{% end_for %}
```
The logic is:

- Wrangle data in a file (aka Python module). In this case, the file is called wrangling.py. The wrangling.py has a function that returns the clean data.

- Execute this function in routes.py to get the data in routes.py

- Pass the data to the front-end (index.html file) using the render_template method.
Inside of index.html, you can access the data variable with the squiggly bracket syntax {{ }}

### Summary Part 2
In the second part, a Plotly visualization was set up on the back-end inside the routes.py file using Plotly's Python library. The Python plotly code is a dictionary of dictionaries. The Python dictionary is then converted to a JSON format and sent to the front-end via the render_templates method.

Simultaneously a list of ids are created for the plots. This information is also sent to the front-end using the render_template() method.

On the front-end, the ids and visualization code (JSON code) is then used with the Plotly javascript library to render the plots.

In summary:

- Python is used to set up a Plotly visualization
- An id is created associated with each visualization
- The Python Plotly code is converted to JSON
- The ids and JSON are sent to the front end (index.html).
- The front end then uses the ids, JSON, and JavaScript Plotly library to render the plots.
