# The Polycule Project

## Goal

To represent the relationships of awesome polyamorous people in graph form and
show how beautifully connected we all are, with proper respect for privacy and
personal identity.

This project was inspired by the gorgeous and complex charts maintained by
[Alex Temple] and [Ray Briggs].  Their work has defined the requirements for
early iterations:

1. **(MVP)** Display the data represented by _Lexi's Polycule Graph_, with a
basic password-locked admin interface for updates and private dissemination.
2. Add additional dimensions to display the data represented by _Ray's Polycule
Graph_, with options to change the visualization.  Allow anonymized public
views and notifications of updates.
3. Allow logins from people whose contact info has been given, and give them
the ability to maintain their own personal information and connections.

Further requirements shall be defined as needed.

## Architecture

## Data Model

### Person

**Attributes:**

* Name (string)
* Pronouns (string, filled by entry form for format consistency)
* List of *Connections (hashlist of pointers?)
* Email address (optional)
* Phone number (optional)

**Methods:**

Getters and Setters
* Person.SetName(string Name)
* Person.GetName() *//returns name as a string*
* Person.SetPronouns(string Pronouns)
* Person.GetPronouns() *//returns pronouns as a string*
* Person.SetPhone(string Phone) *//sets phone number, should be formatted with only digits, hyphens, and optional plus sign if needed for country code*
* Person.GetPhone() *//returns phone number as a string*
* Person.SetEmail(string Email)
* Person.GetEmail() *//returns email address as a string*

Connections
* PersonA.AddConnection(*PersonB, bool Dotted, bool ArrowA, bool ArrowB) *//creates new Connection and adds to both A and B*
* PersonA.AddConnection(*PersonB) *//new solid line with no arrows*
* PersonA.RemoveConnection(*PersonB) *//calls Connection.Remove() on the appropriate Connection*
* PersonA.AddArrowToward(*PersonB) *//calls Connection.AddArrowToward(*Person) on the appropriate Connection*
* PersonA.RemoveArrowToward(*PersonB) *//calls Connection.RemoveArrowToward(*Person) on the appropriate Connection*
* PersonA.IsConnectedTo(*PersonB) *//recursively determines if PersonA is connected to PersonB and returns boolean*

Other
* Person.Notify(string Message) *//sends a notification to preferred contact info, email and/or txt, as selected by user in their settings*
* Person.GetPolycule(int Depth) *//returns a Polycule tree of all Persons connected to the Person, only out to specified depth. Use 0 for no depth limit to retrieve the Person's entire Polycule.*


### Connection

**Attributes:**

* *PersonA (pointer)
* *PersonB (pointer)
* ArrowA (boolean, default 0)
* ArrowB (boolean, default 0)
* Dotted (boolean, default 0)
* Timestamp (set on creation)

**Methods:**

* Connection.GetPersons() *//returns a list of 2 pointers to Persons*
* Connection.IsArrowToward(*Person)
* Connection.AddArrowToward(*Person)
* Connection.RemoveArrowToward(*Person)
* Connection.MakeSolid()
* Connection.MakeDotted()
* Connection.Remove() *//removes pointers from connection lists of persons, then deletes self*


### Polycule

**Attributes:**

* List of *Persons
* PersonCount (determined on creation and updated as needed to save calculation time on render)
* List of *Connections
* ConnectionCount (determined on creation and updated as needed to save calculation time on render)
* List of Pronouns (exhaustive non-redundant list of strings for rendering the key)

**Methods:**

[TO DO - need to write a list of Polycule methods!]

## Contributing
