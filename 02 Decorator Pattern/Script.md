```toc
```

## Format
- Demo size will be 16 pts, from the corner of the screen to touching the start button of the snipping tool. 
- every slide will end with a commented page for if people need to pause it. 

- Thumbnail 
- Background music
- 



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

### Decorator Pattern 1

Let's talk about the Decorator pattern. First of all, how does it work? Think about it as a wrapper. You have the (--)Dark Roast coffee object. Then the customer asks for Mocha, so we create a Mocha object and (--)wrap it around the DarkRoast object. Then the customer asks for milk, so again, we make a milk object and (--)wrap the whole with it.

Since all of this object have a cost function, we can add each of them and come up with the total cost. This is done by first calling the (--)outermost wrapper cost function, Milk, then that function calls the cost function of the (--)next wrapper, Mocha, then that cost function calls the cost function of the (--)next wrapper which happens to be the actual drink, DarkRoast.  And we return (--) the addition of their prices.

It’s a very simple concept but the implementation can be a bit tricky so let’s go over the formal definition and diagram.

### Decorator Pattern 2
The formal definition is (--) the Decorator Pattern attaches additional responsibilities to an object (--)dynamically. (Meaning at runtime) Decorators provide a flexible alternative to subclassing for (--)extending functionality (in other words we’re adding behaviors without touching the code at all!). So, what does that mean, like at the previous example, we’re wrapping an object with another object to give it extra functionality, in our case we were adding each condiment’s price and description to the newly made object.  Now let’s look at the diagram.

The ConcreteComponent  (--)is the object we’re going to dynamically add new behaviors to. It extend Component.  In our system, that would be the individual drinks like espresso, or DarkRoast(--). The ConcreteDecorator  (--) inherits (from the Decorator class) an instance variable for the thing it decorates (the component the decorator wraps). This are going to be our condiments,(--) like Milk or Mocha. Decorators (--) can extend the state of the component. (--) They can also add new methods; however, new behavior is typically added by doing computation before or after an existing method in the component.

The Decorator objects (--) implement the interface or abstract class as the component they are going to decorate. (Meaning every decorated component is going to remain a component object.). Each decorator(--) HAS_A (or wraps) a component, which means the decorator has an instance variable that holds a reference to the  component. And lastly is good to keep in mind that (--)Each component can be used on their own or wrapped by a decorator

### Implementation








