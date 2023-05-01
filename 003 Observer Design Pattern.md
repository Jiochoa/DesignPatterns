Table of Content
```toc
```
---
## Definition

---
## Example

---

## Demo

Structure

-   We introduce a problem (a task)
-   We try to fix it on our own with a brute force approach
-   We state the weaknesses of our solution
-   We introduce the design pattern
-   Fix the problem again with the newly introduced design pattern
-   We talk about all the benefits of the pattern along with the Design Principles that where introduces into it.

Definition explained with real world example.

We got a new task, to make a Weather System.

### Introduction

Hello everyone and welcome to this tutorial on the Observer Design Pattern. In this video we will learn the Observer Pattern with examples and explanations provided mainly by the Head First Design Pattern Book. We will start with a TL;DR for those for you that are in a rush and just want the big picture. So let's get started.

### TL;DR

The Observer Pattern is defined as a one-to-many dependency between objects so that when one object changes, all of its dependencies are notified and updated automatically.

### Observer Pattern

Let’s talk about the stock market. (*) The stocks go up and down and up again, and there's is a lot of money involved so every single change matters, especially to its traders.(*) They are the “dependents“ (*) of the stock market, this is a “one-to-many” relationship because many clients used the Stock Market system. So, it’s very important (*) for them to be automatically notified of every single change (*) because they could be losing(*) a lot of money (*) for every minute they keep a hold of a stock that is dropping rapidly, (*) as well as they could make a lot of money (*) by selling stock on high demand at the right time. (*) Time is very important in this equation. In this system, we could see the Observer Pattern.

### We got a new Task

Imagine you are working at a weather company. Your boss wants you to expand on their current system. Now, let's see what that current system looks like, and what is it that your boss wants you to do. We have a Weather Station (*) this component talks directly with the physical sensor devices of Temperature,(*) Humidity, (*) and Pressure. (*) We also have a WeatherData object (*) who talks to the Weather Station to get the most recent values. We will not go in depth on how it does it, for now, we just need to know that it does. And that’s our current system

Inside the WeatherData class is your task, your boss asks you to implement a measurementChanges (*)function which it should update three different displays, which you also need to make. A current conditions display(*), a weather stats display, (*)and a forecast display(*). He also wants you to make it easy for other developers to make their own displays (*) so they can later charge for them later.

### Do the task with poor design

Now that we have our task,(*) let’s give it a shot.(*) First we need to make the method inside the WeatherData (*). As stated, we are going to call it measurmentsChanges.(*) Then we need to get the most recent values of temperature, humidity, and pressure. Again, we are not concern about how they work, we just need to know that they come from the Weather Station.  We can go on and start updating the displays. We also don’t have the actual displays right now but again, they're not important right now, we're just focusing on the measurmentsChanges function. So we started with the CurrentConditionDisplay and we give it the most recent values for the update. Then we continue on with the StatisticsDisplay, and again we give it the necessary values to update. Lastly, we go to the ForecastDisplay and we do the same and give it what it needs to update.

Now that we have a finished product, let's see what we did right and what we did wrong

### Add the Observer pattern to fix the design

## Demo 

We will begin by implementing the interfaces. Let's start with the Observer. It's pretty simple since it only has one method, `update ()`. With it, it will update the displays with the new information, every display is different, so we're not worried right now about how the Display classes will use it. We move on to the Subject interface. This one has 3 methods, `registerObserver()` which will add a display to the list so the Subject can send them updates, `removeObserver()`, which will remove the selected observer, and `notifyObservers()` which will make sure every observer knows there was a change in the subject. And Lastly, we make the `DisplayElement` interface which will one have one method, `display()` that ensures the displays can show their change.

We move on to the `WeatherData` class which will implement the Subject interface. We're going to keep a list of the observers in a `List` to have a record of every active observer. We will initiate this `List` in the constructor. Since we're using a `List` adding and deleting is very simple we just `add()` and `remove()`. For `notifyObserver()` we will iterate all the observers from the list and call their `update()` method which all observers will have because of the Observer interface. We will call this method in the `measurementChanges()`. Lastly, we need to set the measurements to their most recent value, we will do that with `setMearuements()`, in here we will also call the `measurementChanges()` method which will notify all the observers about this change.

Moving on to the displays, we'll start with the `CurrentConditionDisplay`, this one will implement the Observer and the `DisplayElement` interfaces. We will keep a copy of the weather data, so we can call its add/remove methods. The `update()` will get the current values which will be used on the `display()`. The rest of the Displays are exactly the same, with the exception that they might use only some of the data available. Not all display need to know the pressure, for example.

Now that we have everything ready, let's test our code. We start by making a `WeatherData` object which will communicate with the Weather Station. From there, we can start making the displays, which will automatically register with the given `weatherStation`. Then we give it some random measurements to test it. Let's try that again and run it and see what it gives us. We didnt went trough the specifics of the displays but we can see that it's printing 6 things, and thats because we gave it 2 diferent values and it prints all 3 displays every time theres a change.

## Benefits
Lets talk a little about the benefits we got from the Observer Design Pattern. Without noticing, we started using another Design Principle that is innate to the Observer Pattern. (*) Stive for loosely coupled designs between objects that interact. The only thing the Subject should know about the observer is that (*)it implements the Observer interface and with it, the update() method. Also, we can add new observers at any time because the only thing the subject depends on is in the observers interface so it gives us a lot of freedom on what to do with either the subject or the observers. Another example is that we can reuse the subject and observer, for example by adding another interface without affecting its functionality since they are not tightly coupled.
