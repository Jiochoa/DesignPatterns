```toc
```

## Introduction

Hello everyone and welcome to this tutorial on the Decorator Design Pattern. In this video we will learn the Decorator Pattern with examples and explanations provided mainly by the Head First Design Pattern Book. So, let's get started.


- State the scenario and the problem.
- Try to solve it w/o design pattern.
- Point out the weaknesses of our solution.
- Point out the benefits of the design pattern.
- Introduce the structure.
- Implement the Design Pattern in diagram.
- Code the solution.


### The Problem
Imagine you are working at a Coffee shop that is rapidly growing. When they first went into business, they only had four drinks (--) in the menu, so they carelessly design the system without considering future expansion. The code was very simple, a Superclass (--) called Beverage that would have shared behaviors like the description then the specific drinks would be (--)subclasses which would have the specific description and the cost of the drink. This doesn't seem too bad at first, but what if we want to give clients the option to add Soy milk. We would have to make four more subclasses, since everything is hard coded and there is no way to add ingredients to the drinks. Then what about whipped cream, now we would need (--) eight more classes, considering clients that might want both soy and whipped cream . (--) The problem is very clear now;  we have class explosion. So that's what we need to fix.

### Quick Solution
Now that we have our task, less give it a shot. There are many ways to solve this problem, but let's try adding instance variables to the beverage class to represent new ingredients like milk, soy, mocha, and whipped cream. With the new variables, we will also need getters and setters. Now let's add the subclasses, one for each drink. 

The cost function will be treated a little different this time, because the cost in the Beverage superclass will give you the total cost of the ingredients and the cost in the specific drinks, the subclasses, will give you the total cost of only that drink, so we will need them both.

