# Anti project

Portal Interface

## The user and a language
This section describes who the project would serve and why a language might be a
good way to meet their needs.


### What's the need?

Portal's registration system is a pain in the butt, and everyone knows it. From
the student perspective, we want to

    1. Be able to search for classes
    2. Be able to register for classes
    3. Be able to do the prior two things with low latency

It's not a long list of requirements, but nevertheless the registration system
makes searching for classes difficult, with an interact that doesn't allow
students to easily search based on the criteria that they're interested in
(professors, student availability, etc.). Additionally the system runs with
high latency, and a lot of that is actually spent navigating the interface
(selecting the right subject area, then waiting for the results, then showing
all results, the waiting for all the results, etc.).

### Why a language?

It's seems that a language might be a natural solution to the problem, as
Portal currently suffers from an unwieldy interface and a lack of features. One
could imagine designing a language allows users to do complex searches across
classes and provides results to the in the way they want, the first time.

One could also imagine extending that language to allow for class registration
though it and by providing a scheduling assistant which resolves constraints.

### Why you?

As a Harvey Mudd student, I have a strong interest in a more effective
registration system. I've also spent some time working on Casey Chu's scheduler
application ([here](https://github.com/bitsofpancake/hmc-scheduler)), so I'm a
bit familiar with the systems involved.

I came up with this idea by asking students what made them feel the worst when
they were interacting with computers, and someone brought up portal. Between
that and the general complaints about Portal I feel confident this would be
helping to solve a genuine problem.

### Domain

Course Search and Registration

### Interface (syntax)

One could imagine that the language syntax would be similar to that of SQL for
executing searches, something like:

```
> find CS, taught by Ran, number > 100, when I'm free - sort by number
```

One would also be able to register for classes:
```
> register CS105-1
Registeration for [CS105-1 "Computer System" taught by Geoff Keuning] was
successful!
> register CS105
Ambiguous command. Do you want to register for
0. No class
1. [CS105-1 "Computer System" taught by Geoff Kuening]
2. [CS105-2 "Computer System" taught by Z Sweedyk]
Enter Number > ...
```

Students should also be able to get info on their current schedule and more
detailed information about each class.

One could also set this up as a graphical interface, but the key thing is
that the interface should be flexible and should have a single entry point.

Student want to be able to alternate between dramatically different searches
and even different actions (course details, registration, schedule details)
without having to click through a bunch of buttons and screens.

### Operation (semantics)

When a search is run the system would have to hit the back-end registration
system and perform the requested search. If something about the search could
not be understood, that would be articulated to the user instead of trying to
perform it.

When a register command goes out the program would have to register the student
for that class.

### Expressiveness

It should be easy to find out about classes. It should be easy to register for
classes, it should be easy to get more information about classes.

It should not be Turing complete. It should be hard or impossible to interface
with non-registration related things.


### Related work

Related systems include Casey's
[scheduler](https://github.com/bitsofpancake/hmc-scheduler) (which extends the
Portal interface to help student reconcile class constraints). I like the
schedule resolution this does, but it doesn't really change the UI of Portal at
all, so users have to still click through all the portal windows. I see Casey's
tool as providing a fun new tool rather than changing the way the users
interact with portal.

I think that [SQL](http://dev.mysql.com/doc/refman/5.6/en/sql-syntax.html)
would also be very related.  I imagine that using it as a base to build our
search language off of wouldn't be a bad idea, as SQL has a long track record
of being successfully used by only semi-technical users.

## The Project
This section examines whether the idea makes for a good CS 111 project.


### Suitability
_If someone were to work on this project, what percentage of their time would be
spent directly engaging in the **language** aspects of this project (e.g.,
making language design decisions), as opposed to "systems" aspects of the
project (e.g., implementing a complicated semantics that doesn't require a lot
of language design)?_

I think this is where this idea really falls flat on its face. I think that
most of the work of this project would be on dealing with the course
registration system. The language would probably some sort of cross between a
CLI and SQL, and even if it were done graphically it would probably have a
similar core.

The result is that I think most of the time on this project would be spent
trying to successfully interact with Portal, which is definitely on the
**systems** side of things.

### Scope
_How big an idea is this? How ambitious is this project?_

I think this would actually be a pretty monumental project from the systems
side. Interacting with portal is notoriously impossible to do. This project
might actually end up being forbidden by CIS or the Registrar's Office because
it could potentially mess up students' registration if it had a bug in a
critical situation.

From a language perspective it may actually be a pretty unambitious project. It
seems like some SQL type language would be appropriate for searching, and the
other features would be equally simple.

One thing that might be interesting is setting up a GUI for the SQL queries. I
could imagine typing and having boxes appear, color coordinated by constraint
type.

One could make the project more linguistically ambitious by adding a rules
feature (register for class X if it opens), and then trying to figure out the
best way for users to interact with this feature.

### Benefits and drawbacks
_Why might this be a good idea for a project? Why might this not be a good idea 
project?_

I think that the most appealing part of the project would be the potential
impact. We see a lot of students around us struggle with Portal every time
class registration rolls around, and it would be nice to be able to fix that.

I also find that building CLIs is a very satisfying thing, and ends up having a
larger impact than you might think because then people can use Unix command
line tools to expand your tool in ways that you did not expect. In some sense
you end up making an API that others can use in bigger and better ways.

However, I think this project has a pretty substantial drawback, which is that
it requires only a small amount of linguistic work, and a very large amount of
work behind the scenes to make it function. It's also questionable whether
changing the interface to an existing service is really making a language. I
would say yes because you are changing the way users deliver instructions to
computers, but it could be debated.
