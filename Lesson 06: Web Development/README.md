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

### Summary Part 3
In part 3, the code iterated through the data set to create a visualization with multiple lines: one for each country.

The original code for a line chart with a single line was:
```
graph_one = [go.Scatter(
  x = data[0][1],
  y = data[0][2],
  mode = 'lines',
  name = country
)]
```
To make a visualization with multiple lines, graph_one will be a list of line charts. This was accomplished with the following code:
```
graph_one = []
for data_tuple in data:
   graph_one.append(go.Scatter(
   x = data_tuple[1],
   y = data_tuple[2],
   mode = 'lines',
   name = data_tuple[0]
))
```

### Summary Part 4
In the last part, three more visualizations were added to the wrangling Python module. The wrangling included reading in the data, cleaning the data, and preparing the Plotly code. Each visualization's code was appended to a list called figures. These visualizations were then imported into the routes.py file. This figures list was sent from the back end to the front end via the render_template method. A list of ids were also sent from the back end to the front end.

Then on the front end (index.html), a div was created for each visualization's id. And with help from the JavaScript Plotly library, each visualization was rendered inside appropriate div.

### Beyond a CSV file
Besides storing data in a local csv file (or text, json, etc.), you could also store the data in a database such as a SQL database.

The database could be local to your website meaning that the database file is stored on the same server as your website; alternatively, the database could be stored somewhere else like on a separate database server or with a cloud service like Amazon AWS.

Using a database with your web app goes beyond the scope of this introduction to web development, here are a few resources for using databases with Flask apps:

- [Tutorial - Using Databases with Flask](https://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-iv-database)
- [SQL Alchemy- a Python toolkit for working with SQL](https://docs.sqlalchemy.org/en/20/)
- [Flask SQLAlchemy - a Flask library for using SQLAlchemy with Flask](https://flask-sqlalchemy.palletsprojects.com/en/2.x/)

### Instructions Deploying from the Classroom
Here is the code used in the screencast to get the web app running:

First, a new folder was created for the web app and all of the web app folders and files were moved into the folder:
```
mkdir web_app
mv -t web_app data worldbankapp wrangling_scripts worldbank.py
```
The next step was to create a virtual environment and then activate the environment:
```
conda update python
python3 -m venv worldbankvenv
source worldbankenv/bin/activate
```
Then, pip install the Python libraries needed for the web app
```
pip install flask pandas plotly gunicorn
```
The next step was to install the heroku command line tools:
```
curl https://cli-assets.heroku.com/install-ubuntu.sh | sh
https://devcenter.heroku.com/articles/heroku-cli#standalone-installation
heroku —-version
```
And then log into heroku with the following command
```
heroku login
```
Heroku asks for your account email address and password, which you type into the terminal and press enter.

The next steps involved some housekeeping:

- remove app.run() from worldbank.py
- type cd web_app into the Terminal so that you are inside the folder with your web app code.
Then create a proc file, which tells Heroku what to do when starting your web app:
```
touch Procfile
```
Then open the Procfile and type:
```
web gunicorn worldbank:app
```
Next, create a requirements file, which lists all of the Python library that your app depends on:
```
pip freeze > requirements.txt
```
And initialize a git repository and make a commit:
```
git init
git add .
git commit -m ‘first commit’
```
Now, create a heroku app:
```
heroku create my-app-name
```
where my-app-name is a unique name that nobody else on Heroku has already used.

The heroku create command should create a git repository on Heroku and a web address for accessing your web app. You can check that a remote repository was added to your git repository with the following terminal command:
```
git remote -v
```
Next, you need to push your git repository to the remote heroku repository with this command:
```
git push heroku master
```
Now, you can type your web app's address in the browser to see the results.
