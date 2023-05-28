### Introduction

Hello and welcome to this tutorial series on Software Design Patterns. In this video we will learn the Observer Design Pattern, with examples and descriptions provided mainly by the Head First Design Pattern Book. So, let's get started.

### Scenario
#### Part 1
Imagine you are working at a weather company (-1-). Your boss gives you a new task (-2-), she wants you to create an app that uses the WeatherData object , (-3-) which will be provided by the company, to update the three different displays, one for current conditions, another one for weather stats, and another one for forecast.(-4-) Now, let's see what we have available. We have a Weather Station (-5-) this component talks directly with the physical sensor devices of Temperature,(-6-) Humidity, (-7-) and Pressure. (-8-) We also have the WeatherData object (-9-) who talks to the Weather Station to get the most recent values. (-10-)We will not go in depth on how it does it, for now, we just need to know that it does. With your help, this WeatherData object will be the one to update the Current Condition(-11-) display, the Weather Stats display (-12-)and the Forecast Display(-13-). Now let’s take a look at what’s inside the WeatherData object

#### Part 2
Inside of it, we have the three methods (-1-), getTemperature, getHumidity and getPressure, that will get the most recent values from the Weather Station. Also, this is where we will create a new function, (-2-) measurementsChanges(), and this is where we will accomplish the task. As stated, the function should update the three different displays, which are not strictly part of the task but we will make them for testing purposes. And that, is the sum of our current system. So, let’s get to work.

### Uneducated Solution
#### Part 1
Now that we have our task, let’s give it a shot.(-1-) First we find the method inside the WeatherData. As stated, it’s called measurmentsChanges. (-2-) Then we need to get the most recent values of temperature, humidity, and pressure. Again, we are not concern about how they work, we just need to know that they work and that they come from the Weather Station. (-3-)  We can go on and start updating the displays. We also don’t have the actual displays right now but again, they're not important right now, we're just focusing on how the measurmentsChanges function is going to work. So, we started with the CurrentConditionDisplay and we give it the most recent values for the update. Then we continue on with the StatisticsDisplay and again we give it the necessary values to update. Lastly, we go to the ForecastDisplay and we do the same and give it what it needs to update.
Now that we have a finished product lets analyze the results.

#### Part 2
It doesn’t look too bad, after all, we accomplished out task, but there are a few things wrong with this implementation, lets go over them. First of all, we hardcoded the displays(-1-) therefore we cannot add or remove new displays without going back to the code which is not good for new developers, we need to add some flexibility to it. A good fix would be to extract them, since they are the most likely to change. All three displays are using the same update method, so we did do a few things right, although not entirely correct because what if in the future we add a new sensor to the Weather station, wind speed for example.  Our system wouldn’t be able to handle that, so we need another fix for that too. Let’s talk a little about the Observer Pattern.

### Formal Pattern
#### Part 1
The formal definition is The Observer Pattern is Defined as a one-to-many dependency between objects so that when one object changes, all of its dependents are notified and updated automatically. Let’s take it bit by bit. It is a (-1-) “one-to-many dependency between objects” so we have many objects (-2-) depending one object (-3-) for at least one specific thing, like a function. Moving on, (-4-)“so that when one object changes, all of its dependents are notified and updated automatically.” So, the dependents are giving the dependee enough power over them (-5-) to control their updates.(-6-) Now let’s look at its class diagram

#### Part 2
We have the Subject interface. (--) This is what Observer use when they wants to register as an Observer to this specific Subject or when they wants to remove themselves from the Observer list. Then we have the Observer interface, (--) all potential Observers must implement, It only has one method which will be called every time the Subject updates. As stated, it is a one-to-many dependency so one Subject can have many Observers. (--) We also have their concrete classes. Starting with the ConcreteSubject, they must implement the Subject interface. Not only to register and remove observers, they also have the task of notifying Observers every time they have an update or change state, and they do that with the notifyObservers method. It is common to also have a getters and setters for the state of the concrete subject but that is another design Pattern, more of that in a future video. And last, we have the concrete observers, which has a lot less restrictions because although it has to use the Observer interface, it only has one method to implement. This method will be called by the subject every time it updates.
If we follow this design, every time the concreteSubject changes state, it will notify all the observer objects and call their update method.

### Solve the Problem with the DP

We start by making the WeatherData into the ConcreteSubject (--) since according to our task, it should be in charge of updating the Displays. What about the observers, in this scenario we will start with 3 observers which will be the individual displays, (--) since they are the ones interested in getting the most recent values. Another thing to consider is that all the Displays implement the display method, so to make it easier to test we will also include a (--) DisplayElement interface, but keep in mind that this is not part of the Observer Pattern, this is just for us. And that, is the sum of our system, now we just need to code it.

### Demo
#### Part 1: interfaces
We start by making the WeatherData into the ConcreteSubject (--) since according to our task, it should be in charge of updating the Displays. What about the observers, in this scenario we will start with 3 observers which will be the individual displays, (--) since they are the ones interested in getting the most recent values. Another thing to consider is that all the Displays implement the display method, so to make it easier to test we will also include a (--) DisplayElement interface, but keep in mind that this is not part of the Observer Pattern, this is just for us. And that, is the sum of our system, now we just need to code it.

#### Part 2: WeatherData
We move on to the WeatherData class. First, we make it implement the Subject interface. Then we start making some instance variables, starting with a list of observers. Then we initiate the sensor variables for later use. The constructor will simply define the list as an Array object, this will keep it flexible enough to add and remove observers. We move on to implementing the methods on the Subject interface starting with registerObserver, which is very simple. We just need to add it to the observers array. As for the removeObserver we just remove it too. For the notifyObservers we will iterate the observers list and call all of their update function. Notice that we don’t care about the individual class besides of the Observer method. Next is the measuremenrsChanges, as stated by your boss, this is the method that should notify the observers, so what we’ll do is just make it call the notifyObservers method since it’s already taking care of it. Then we make another method to get the most recent sensor values, setMeasurements. This would normally call the getTemperture, getHumidity and getPressure methods but for testing purposes we will just hardcode the values. We will also notify the system of value changes in this method.

#### Part 3: CurrentConditionDisplay
Moving on to the displays, we'll start with the CurrentConditionDisplay, this one will implement the Observer and the DisplayElement interfaces. We will keep a copy of the weather data, so we can call its add/remove methods. The update() method will get the current values which will be used on the display() method. The rest of the Displays are exactly the same, with the exception that they might use only some of the data available. Not all display need to know the pressure, for example.

#### Part 4: Testing
Now that we have everything ready, let's test our code. We start by making a `WeatherData` object which will communicate with the Weather Station. From there, we can start making the displays, which will automatically register with the given `weatherStation`. Then we give it some random measurements to test it. Let's try that again and run it and see what it gives us. We didn't went trough the specifics of the displays but we can see that it's printing 6 things, and thats because we gave it 2 diferent values and it prints all 3 displays every time theres a change.

### Benefits

Alight, We just made a bunch of changes, we wrote about double the amount of code as our first solution, so it doesn’t seem too productive. But why? It goes back to the first thing we learned about programming, that code will always change over time. The more successful the program the more changes are to be expected.  So we need to prepare for them. Without noticing, we started using another Design Principle that is innate to the Observer Pattern. (*) Stive for loosely coupled designs between objects that interact. The only thing the Subject should know about the observer is that (*)it implements the Observer interface and with it, the update() method. Also, we can add new observers at any time because the only thing the subject depends on is in the observers interface so it gives us a lot of freedom on what to do with either the subject or the observers. Another example is that we can reuse the subject and observer, for example by adding another interface without affecting its functionality since they are not tightly coupled.

### Outro

And that’s it for this video. Thank you for watching. If you have any questions, leave them in the comment section.

this is a test. 



