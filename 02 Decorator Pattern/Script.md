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
Now that we have our task, let's give it a shot. There are many ways to solve this problem, but let's try adding instance variables (--)to the beverage class to represent the condiments (--) like milk, soy, mocha, and whipped cream. With the new variables, we will also need (--) getters and setters, so we can add them to the drinks, and of course the (--) prices. The biggest difference will be in the (--)cost function. The original one was an abstract function, this new one will only return the prices of the condiments, and we will leave the cost of individual drinks to be calculated on their respective subclasses. We will do this by checking if a specific condiment was included and if true, it will be added to the total cost. At the end, it will return the price of all the included condiment. 

Now let's add the subclasses, one for each drink. The only difference here will be in the cost function. Aside from its cost, we will add the superclass cost, which is the condiments.

### What’s wrong with Solution 1
Now that we have our system(--), let’s test it, let’s do an Expresso with soy milk and mocha.  (--) We make a Beverage object, and we’ll call it drink1, then we’ll make it an expresso, then we add the soy milk, and last we add the mocha.  Now, lets print it. Seems to be working.

It doesn’t look too bad, we accomplished out task after all, but there are a few things wrong with this implementation, lets go over them. What if the customer wants a double mocha? (--)Our system has only true and false (--) for each condiment so we would have to go to the code and change it to accept more. (--)What if the price of the condiments change? Again, we would have to go to the code. What about including drink sizes,(--) or adding new condiments like vanilla? Our system is not prepared for change.

### Decorator Pattern

Let's talk about the Decorator pattern. First of all, how does it work? Think about it as a wrapper. You have the a Dark Roast co
