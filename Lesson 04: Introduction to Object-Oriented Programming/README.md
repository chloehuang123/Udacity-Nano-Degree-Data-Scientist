# Lesson 04: Introduction to Object-Oriented Programming

### Object-Oriented Programming (OOP) Vocabulary
class - a blueprint consisting of methods and attributes

object - an instance of a class. It can help to think of objects as something in the real world like a yellow pencil, a small dog, a blue shirt, etc. However, as you'll see later in the lesson, objects can be more abstract.

attribute - a descriptor or characteristic. Examples would be color, length, size, etc. These attributes can take on specific values like blue, 3 inches, large, etc.

method - an action that a class or object could take

OOP - a commonly used abbreviation for object-oriented programming

encapsulation - one of the fundamental ideas behind object-oriented programming is called encapsulation: you can combine functions and data all into a single entity. In object-oriented programming, this single entity is called a class. Encapsulation allows you to hide implementation details much like how the scikit-learn package hides the implementation of machine learning algorithms.

In English, you might hear an attribute described as a property, description, feature, quality, trait, or characteristic. All of these are saying the same thing.

Here is a reminder of how a class, object, attributes and methods relate to each other.

### Function vs Method
In the video above at 1:44, the dialogue mistakenly calls init a function rather than a method. Why is init not a function?

A function and a method look very similar. They both use the def keyword. They also have inputs and return outputs. The difference is that a method is inside of a class whereas a function is outside of a class.

### What is self?
If you instantiate two objects, how does Python differentiate between these two objects?
```
shirt_one = Shirt('red', 'S', 'short-sleeve', 15)
short_two = Shirt('yellow', 'M', 'long-sleeve', 20)
```
That's where self comes into play. If you call the change_price method on shirt_one, how does Python know to change the price of shirt_one and not of shirt_two?
```
shirt_one.change_price(12)
```
Behind the scenes, Python is calling the change_price method:
```
    def change_price(self, new_price):

        self.price = new_price
```
Self tells Python where to look in the computer's memory for the shirt_one object. And then Python changes the price of the shirt_one object. When you call the change_price method, shirt_one.change_price(12), self is implicitly passed in.

The word self is just a convention. You could actually use any other name as long as you are consistent; however, you should always use self rather than some other word or else you might confuse people.

[Exercise: OOP Syntax Practice - Part 1]()