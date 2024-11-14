# Object-Oriented Design

Step 1: Handle Ambiguity
- questions are often intentionally vague
- ambiguity is present to see whether or not you will make assumptions or ask clarifying questions
- ask probing questions to figure out the complexity and scope
    - who, what, when, where, why, how

Step 2: Define Core Objects
- identify what the major components of the system are
- e.g. restaurant contains the objects: table, guest, party, order, meal, employee, server, host

Step 3: Analyse Relationships 
- which objects are members of which other objects
- do any objects inherit form any others
- are relationships many-to-many or one-to-many

Step 4: Investigate Actions
- consider key actions that th eobject will take and how they relate to each other
- these actions can be translated into an objects respective functions


Design Patterns:

Singleton:
- ensures a class has only one existing instance and ensures access to the instance globally across the appliaction
- some consider it to be the "anti-pattern" due to it interfering with unit testing

Factory Method:
- creating an instance of a class, with its subclasses deciding what class to instantiate