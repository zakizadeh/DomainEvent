# DomainEvent
Domain Events in .Net

“A Domain Event captures the memory of something interesting which affects the domain “
— Martin Fowler
Domain Events are used to allow aggregates to react to a change in another aggregate without coupling them. Pioneering DDD books from the likes of Eric Evans and Vaughn Vernon advocate using asynchronous mechanisms for handling Domain Events. However, this hugely increases the complexity of your applications and the number of components that you must host due to a proliferation of Event Handlers.

I have written a sample .NET application for a fake eCommerce company named DDDMart.
The application focuses on the core domain layer so does not have any APIs. There are a lot of different opinionated ways to host domain models through an API and I specifically wanted to focus on modelling the domain and how Domain and Integration events are handled.

Architecture
0.Framework = DomainEventDispatcher
1.Core = 
- Domain = entities and events  
- ApplicationServices =  DomainEventHandler
2. Infra = CustomDbContext
3.Endpints = PersonController
Scenario
The sample simulates the following scenario:
A person is added and PersonCreated event is raised.
Before the save change is done, WitePersonCreatedToFile Handler is Dispatched and the person is written in a text file.




you can see the scenario in detail in following picture:

![eventsourcingdiagram](https://github.com/zakizadeh/DomainEvent/assets/11499371/c43adbbf-dfcd-42cb-9b9a-c423de8ad798)


The complete process looks like this:

. Create database transaction.

. Get aggregate(s).

. Invoke aggregate method.

. Add domain events to Events collections.

. Publish domain events and handle them.

. Save changes to DB and commit transaction.
