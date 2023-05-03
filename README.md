Download Link: https://assignmentchef.com/product/solved-cs2030s-lab-1-simulation-i
<br>
In this lab, the goal is for you to practice the basic OOPprinciples: encapsulation (including tell-don’t-ask andinformation hiding), abstraction, inheritance, andpolymorphism.

You are given six classes: five Java classes and one main`Lab1` class. Two of them are poorly written withoutapplying any of the OOP principles. You should rewritethese two classes using the OO principles you have learned,removing them and creating new classes as needed.

## Background: Discrete Event Simulator

A discrete event simulator is software that simulates asystem (often modeled after the real world) with events andstates. An event occurs at a particular time and each eventalters the states of the system and may generate moreevents. A discrete event simulator can be used to study manycomplex real-world systems. The term discrete refers to thefact that the states remain unchanged between two events,and therefore, the simulator can jump from the time of oneevent to another, instead of following the clock in realtime.

In Lab 1, we provide you with three very generic classes:`Simulator`, which implements a discrete event simulator,`Event`, which encapsulates an event (with a time), and`Simulation`, which encapsulates the states we aresimulating. The `Event` and `Simulation` class can beextended to implement any actual simulation (network, roadtraffic, weather, pandemic, etc). More details of theseclasses can be found below.

## Simulating a Shop

In Lab 1, we wish to simulate a shop. A shop can haveone or more service counters.

In the beginning, all service counters are available. Acounter becomes unavailable when it is serving a customer,and becomes available again after servicing a customer.

A customer, upon arrival at the shop, looks for the firstavailable counters for service. If no counter is available,the customer departs (due to COVID-19, no waiting isallowed). Otherwise, the customer is served, and afterbeing served for a given amount of time (called servicetime), the customer departs.

Two classes, `ShopSimulation` (a subclass of Simulation)and `ShopEvent` (a subclass of Event) are provided. Thetwo classes implement the simulation above.

## The `Event` class

You should not edit this class. The following is for yourinfo only.

The `Event` class is an abstract class with a single field`time`, which indicates the time the event occurs. The`Event::toString` method returns the time as a string andthe `Event::getTime` method returns the time.

The most important thing to know about the `Event` class isthat it has an abstract method `simulate` that needs to beoverridden by its subclass to concretely define the actionto be taken when this event occurs.

Simulating an event can lead to more events being created.`Event::simulate` returns an array of `Event` instances.

## The `Simulation` class

You should not edit this class. The following is for yourinfo only.

The `Simulation` class is an abstract class with a singlemethod `getInitialEvents`, which returns an array of eventsto simulate. Each of these events may generate more events.

## The `Simulator` class

You should not edit this class. The following is for yourinfo only.

The `Simulator` class is a class with only two methods andit is what drives the simulation. To run the simulator, weinitialize it with a `Simulation` instance, and then call`run`:

“`Simulation sim = new SomeSimulation();new Simulator(sim).run();“`

The `Simulation::run` method simply does the following:

– It gets the list of initial `Event` objects from the`Simulation` object;– It then simulates the pool of events, one-by-one in theorder of increasing time, by calling `Event::simulate`;– If simulating an event resulted in one or more new events,the new events are added to the pool.– Before each event is simulated, `Event::toString` is calledand a message is printed– The simulation stops running if there are no more events tosimulate.

For those of you taking CS2040S, you might be interested toknow that the `Simulator` class uses a priority queue tokeep track of the events with their time as the key.

## The `ShopSimulation` class

You are expected to edit this class and create new classes.

The `ShopSimulation` class is a concrete implementation ofa `Simulation`. This class is responsible for:

– reading the inputs from the standard inputs,

– initialize the service counters (represented with boolean`available` arrays)

– initialize the events corresponding to customer arrivals

– return the list of customer arrival events to the`Simulator` object when `getInitialEvent` is called.

Each customer has an id. The first customer has id 0,The next one is 1, and so on.

Each counter has an id, numbered from 0, 1, 2, onwards.

## The `ShopEvent` class

You are expected to _replace_ this class with new classes.

The `ShopEvent` class is a concrete implementation of`Event`. This class overrides the `simulate` method tosimulate the customer and counter behavior.

A `ShopEvent` instance can be tagged as either an arrivalevent, service-begin event, service-end event, or departureevent.

– Arrival: the customer arrives. It finds the firstavailable service counter (scanning from id 0 upwards) andgo to the counter for service immediately. Aservice-begin event is generated. If no counter isavailable, it departs. A departure event is generated.

– Service-begin: the customer is being served. Aservice-end event scheduled at the time (current time + servicetime) is generated.

– Service-end: the customer is done being served and departsimmediately. A departure event is generated.

– Departure: the customer departs.

## Inputs and Outputs

The main program `Lab1.java` reads the following, from thestandard inputs.

– An integer n, indicating the number of customers to simulate.

– An integer k, indicating the number of service counters theshop has.

– n pairs double values, each pair corresponds to a customer.The first value indicates the arrival time, the secondindicates the service time for the customer.

The customers are sorted in increasing order of arrival time.

## Assumptions

We assume that no two events ever occur at the same time.As per all labs, we assume that the input is correctlyformatted.

## Your Task

The two classes, `ShopSimulation` and `ShopEvent`, arepoorly written. They do not fully exploit OOP features andapply the OO principles such as abstraction, encapsulation(including information hiding and tell-don’t-ask), composition,inheritance, polymorphism, and LSP.

Rewrite these two classes (adding new ones as needed) with theOOP principles that you have learned:

– encapsulation to group relevant fields and methods intonew classes

– inheritance and composition to model the relationshipbetween the classes

– information hiding to hide internal details

– using polymorphism to make the code more succinct andextendable in the future, while adhering to LSP

Here are some hints:

– Think about the problem that you are solving: what arethe nouns? These are good candidates for new classes.

– For each class, what are the attributes/properties relevantto the class? These are good candidates for fields in theclass.

– Do the classes relate to each other via IS-A or HAS-Arelationship?

– For each class, what are their responsibilities?What can they do? These are good candidates for methods inthe class.

– How do the objects of each class interact?These are good candidates for public methods.

– What are some behavior that changes depending onthe specific type of objects?

Note that the goal of this lab and, and of CS2030S ingeneral, is _NOT to solve the problem with the cleverest andthe shortest piece of code possible_. For instance, you mightnotice that you can solve Lab 1 with only a few variablesand an array. But such a solution is hard to extend andmodify. In CS2030S, our goal is to produce software thatcan easily evolve and be modified, with a reduced risk ofintroducing bugs while doing so.

Note that Lab 1 is the first of a series of labs, where weintroduce new requirements or modify existing ones in everylab (not unlike what software engineers face in the realworld). We will modify the behavior for the shop, thecounters, and the customers. In particular, in the future,

– a customer may have different behavior in selecting thecounters to join.– a shop may have different rules about managing customerswhen the COVID-19 pandemic is over, including introducingdifferent types of counters.

Thus, making sure that your code will be able to adapt tonew problem statements is the key. Trying to solve the labwithout considering this and you will likely find yourselfpainted into a corner and have to re-write much of yoursolution to handle the new requirement.