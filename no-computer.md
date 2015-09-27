# No computer project

Running Routes for the Hash House Harriers

## The user and a language
This section describes a potential language, the group it serves, and some
attributes of how the potential language is used.

### What's the need?

Periodically the organization know as the Hash House Harriers likes to lead fun
running events. On such an event the organization would like to
   1. Have one or two of its members come up with a set of activities for such
      a run, along with a theme. That group, the _hares_ are responsible for
      making a route and communicating it to the rest of the group, the
      _hounds_.
   2. Have the hounds understand and follow the route, doing fun activities
      along the way.

Preferably the route will also have constructs which keep the hounds moving as
a group, regardless of athletic ability.

### How is this need met?

The Hash House Harriers solve this problem which I am going to presumptuously
call the Hashing Language (HL). It is a formal system of communication from the
hares to the hounds.

### What brought this to your attention?

I've been both hare and hound many times.

### Domain

Hash House Harriers Running Club

### Interface (syntax)

A HL 'program' (called a _route_ from here on out) is composed of chalk
markings on the group. These chalk marking form a number of units of meaning:
   * [ON-ON](http://www.sumopaint.com/images/temp/xzklpdnixrdrpocl.png) - the
     beginning of a route.
   * [Multi-Arrows](http://www.sumopaint.com/images/temp/xztrkqocqnmablqs.png)
     are used at a regroup or ON-ON. They offer multiple routes, only 1 is 
     real.
   * [Arrow](http://www.sumopaint.com/images/temp/xztbfkqaacscdpln.png) - the
     path is in this direction
   * [Falsy](http://www.sumopaint.com/images/temp/xzfpoddofmgoqkis.png) -
     marks a false path! Go back to the last set of multi-arrows.
   * [Regroup](http://www.sumopaint.com/images/temp/xzakkncxrfefpjbf.png) -
     wait for the group and do an activity with everyone
   * [Turkey Eagle](http://www.sumopaint.com/images/temp/xzrrtdejhdtnhjhs.png)
     used to indicate an easy and hard path, hounds each choose one.
     Followed by the paths eventually joining.
   * [BVC](http://www.sumopaint.com/images/temp/xzkritmbkfjnhjpc.png) - warns
     hounds to be very careful on stairs, in streets, etc.
   * [ON-IN](http://www.sumopaint.com/images/temp/xzrhifdistbcmeit.png) -
     indicates the end of the route.

Activities can also refer to a number of known concepts for specifying who
should do an activity:
   * FRB[xN] - 'Front Running Bastard' (or first N people).
   * DFL[xN] - 'Dead Fucking Last' (or last N people).
   * N - the number of people on the hash.

HL routes thus consist of chains of these symbols linked by arrows. Programs
can be written well (arrows line up cleanly) or contain errors (arrows do not
line up).

### Operation (semantics)

An HL route is executed by being followed by the hounds. In this sense it is
interpreted rather than compiled - no holistic check of the route is done
before it begins executed.

The hounds follow the route to the best of their ability, much the same as a
computer follows assembly instructions. Many types of errors can occur.

HL routes can be malformed - for example lines instead of arrows, or not
re-uniting the turkey and eagle paths. They can also be well-formed, but
produce undesired behavior - for example having a loop of arrows :wink: or
early arrows may lead the hounds to late arrows, skipping the middle section
of the route altogether.

### Why is it a language?

HL is a language for three reasons.

It is a standardized method of communication, governed by rules and unambiguous
when used correctly.

It is written by one entity (the hares) and thus used by that entity to
the behavior of another entity (the hounds).

It has fundamental units which allow for composition into arbitrarily complex
routes. In this way novel routes can be written forever.

### Expressiveness

Leading people along routes is very easy in HL. One might imagine getting a
computer to follow such a route would be very difficult.

HL also makes it difficult to lay routes in some areas, including:

   * Indoors
   * Over slippery surfaces where chalk doesn't stick
   * Over grass
   * Over gravel
   * In water, although sometimes it works out well (the CMC cube fountain)

These may not be desired difficulties, but nevertheless they exist because of
the constraints of chalk.

### Related work

A related language is the version of HL which is created using bue tape and
paper. This version of the language exists to solve some of the above problems,
notably by giving a way to write HL indoors.

Sometime HL will also be written using whiteboard markers or blackboard chalk,
depending on what is available indoors.

## The Project
This section examines whether the idea makes for a good CS 111 project.


### Suitability

I'm not actually very sure if this would make a good DSLs project. Mot of the
limitations in the current use of the language seem systems-y - more related to
the medium in which the language is written than the actually form of the
language itself.

Notably the most pressing issues are how to write HL indoors and on rough
terrain, which seem to be more problems of finding a way to leave messages
indoors that are temporary and do not annoy the users of the indoor space.

One neat idea might be to try to leave electronic messages. Perhaps the hares
could mark out a path on some sort of map interface and that path could be
incrementally displayed to the hounds as they progress along it. Activities
could be left as waypoints on the map. This seems somewhat technically
challenging, but if a lot of the GPS stuff could be handled by a library there
might end up being enough time left over to think making the experience of
setting a hash as good as possible.

### Scope

Whether the electronic redesign of the language would be of an appropriate
scope is very dependent on the difficulty of implementation - I think the
linguistic part of it would be very doable (mostly thinking about
making a really smooth UI that allows hares to communicate routes effectively).
The application would have to be written as either a very versatile web-app or
as a native application on Android/iOS. I think either one would be pretty
challenging to do, and I think that ultimately this would be more
implementation work than is appropriate or feasible for a DSLs project.

### Benefits and drawbacks

One of the benefits of this project would be getting to work on an intensely
spatial language that interfaces heavily with the real world. Most programming
languages interface with computer screens at their very most spatial, so trying
to help people mark paths on the real world would be pretty novel and
interesting.

I think the scope of the technical challenges this project poses would
definitely be a drawback - spending a bunch of time getting GPS to work or
struggling with Android/iOS isn't really the intent of the class.

I also think that there isn't a lot of demand for an electronic version of the
language. Hashers seem pretty content with what they have, and someone doing
this project would really have to been down what advantages the electronic
version would have. In particular, an electronic version seems like it would
clash with the old ideal of hounds chasing the hares in real time as the lay
the route (although many people lay it in advance anyway).

