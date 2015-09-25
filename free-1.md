# Free project 1

Geometric Drawings

## The user and a language
The user for this project is someone who wants to make geometric drawings.
They might be a teacher, making drawings for handouts, slides, homework
problems, or exam problems. They might be a researcher either geometric or in
a related field trying to make a drawing to explain an idea, or perhaps making
a drawing as a part of figuring out their ideas.

Notably these people are careful and analytical, but they may not be
computer-savvy.

I want to build a language that allows them to make these drawings in a way
that saves time and feels natural to them.

### What's the need?

The need is to create drawings, usually to be embedded in some sort of text
document, but not always.

Right now people do this in a few ways. The high school teachers I know use
various plugins for Microsoft Word that have graphical interfaces. Others
choose to use LaTeX and systems built on `tikz` like `tkz-euclid`, found
[here](https://www.ctan.org/pkg/tkz-euclide?lang=en).

The graphical interfaces are nice in some situations, but ambiguities emerge
sometimes, because the only input to the program is (x,y) position, it may not
always be clear what geometrically significant idea that location corresponds
to. For example, if I draw a line from one angle of a triangle to the other
side, am I drawing to the side's midpoint or bisecting the angle? These are
usually not the same, but are close to each other!

The tkz-euclid solution on the other hand, has a static textual interface. You
can draw lines, draw shapes, and label intersections. The system is
impressively complete, but seems cryptic at times. It is not clear how to do
things like find an intersection, and more generally you don't always know what
options are available to you. Furthmore, the names of the language correspond
vaguely to the mathematical writing that they are based on, but are heavily
constrained by LaTeX

I would like to create an experience that allows for more complete interaction
between the user and the computer. It would be awesome to allow for users to
express what they would like to draw in a language and syntax that feels
natural to them, while also getting visual feedback about what they're drawing
and what they could choose to do next.

### Why a language?

I think that I should address this question in two parts:
1. This question should be solved with a DSL because geometric writing is
   already designed to unambiguously communicate geometric constructions. There
   we should try to teach computers how to understand that language, or
   something similar to it.
1. Why interactive? Is making something interactive really part of DSLs? Is
   making something interactive really changing the language? I argue yes.
   Language is fundamentally a framework for communication. To me it seems odd
   that programming languages so far hav just been about users telling
   computers what to do. Allowing for computers to give feedback to users
   expands the language to allow for 2-way communication. And the way the
   computer sends back information will need to be designed well to make it
   most useful to the users.

### Why you?

I've always enjoyed geometry, and am excited about building an interactive
system which makes computers a better platform for exploring mathematical ideas
that are not fully formed yet.

### Domain

Interactively creating geometric drawings

### Interface (syntax)

Users could interact with the language statically or interactively.

In either case they would write statements like:

```
circle x with center C
line y tangent to C at point D
line z through points C and D
```

I really like language idea because it mirrors the way that mathematicians
write about geometry. Who hasn't seen something like:

Let x be a circle centered at C. Let y be a line tangent to x at point D. Let z
be a line through C and D. ...more proof...

### Operation (semantics)

So operation would work in two ways.

The first of these is the static mode. People write stuff like above and
trigger compilation which generates an image or LaTeX code, or something like
that.

The more intersting would be interactive mode, where as the users enter each
line the image is drawn for them to see what they have, as well as to indicate
potentially intersting thing to do next (IE, higlighting the tangent point
after drawing a tangent). Using this information the users can issue special
interactive commands that act on those possibilities.

At the end of the session the user could export the image, LaTeX, or DSL code
that would have created the image they ended up creating interactively.

### Expressiveness

It should be easy (and should feel natural) to make simple geometric drawings
and format them in simple ways (rotation, size, cropping, labelling, etc).

It should be hard to make really complex drawings with lots of parts. Visual
clutter is not something that is desirable in geometry.

It should be impossible/extremely difficult to simulate a turing machine. This
language is not for computation. In the end it is an assistive formatting
language.

It would also be cool to allow for sub-routines. People should be able to
define, "Find the centroid of this triangle" and re-use that idea without
having to redo all the work.

### Related work

There are a lot of interesting graphical drawing aides.

For example [Sketchometry](http://start.sketchometry.org/). These all do well
in that they are graphical and are thus easy to start using, but they run into
problems with when geometrically distinct ideas are spatially close (as
discussed above).

There is also the `tkx-euclid` LaTeX package. It seems to be very complete, and
has seems to have a good underlying geometric model, but it is somewhat
cryptic, doesn't look _that much_ like geometric writing, and it is sometimes
unclear what options the user has (Did the thing I drew intersect with
something else?).

## The Project
This section examines whether the idea makes for a good CS 111 project.


### Suitability

There is some question here. I think that the time would probably end up being
split 50/50, although that would change depending on whether I could find a
good geometry library that would meet most of my needs (shape drawing and
intersection detection come to mind right now, but I imagine the list will
grow). The language design time would be spent thinking about syntax for use
input, thinking about how the computer will provide feedback to the users, and
thinking about the users should be able to incorporate that feedback into
further instructions.

If I were building this from the ground up this would probably be way to
**systems** heavy.

I think if on doesn't accepted the computer feedback and user response to that
feedback as part of the language, this proect would be entirely unsuitable.
Because I think language is a 2-way street, I would say that it is suitable
(see the [Why a Language](#whyalanguage) section.

### Scope

It's always hard to answer this question. I think this is a project of moderate
scope - it would not be easy, but also can be accomplished.

I think that I may end up being forced into some sort of external DSL because
of the interactive constraints, but I can probably still lean heavily on things
like Scala for execution.

### Benefits and drawbacks

I think this would be an awesome project because it would explore the idea of
making  DSL not just a way for a user to provide instructions for the computer,
but also a way for the computer to 'talk back'.

It reminds me of a research project a friend of mine was working on, the goal
of which was to have programs be generated after some sort of 'conversation'
between the user and computer.

I think that a drawback would be that doing all the human-computer interaction
stuff may end up drowning out some of the finer points of syntax that DSL
design traditionally focusses on.

I also think this project is not semantically trivial. While it's not a
deal-breaker, it would be nice to be able to focus entirely on the language
design.

I also think this project addresses a very narrow domain, and that domain may
not feel the need for a new tool. While I would enjoy having an interactive
system for making drawings, many users may be happy with graphical or TeX-based
solutions.
