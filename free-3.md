# Free project 2++

[I see **trees** of green](https://www.youtube.com/watch?v=A3yCcXgbKrE)

## The user and a language
This section describes who the project would serve and why a language might be a
good way to meet their needs.


### What's the need?

The users I have in mind for this DSL are programmers who are interested in
rapidly writing binary tree algorithms. They want to be able to test out ideas
quickly and elegantly, and may not care very much about systems-level
optimizations.

Right now they people probably write a lot of boilerplate code for each tree
they write, including the structure of nodes, code for tree rotations,
debugging tools and more.

Furthermore the details of some of the boilerplate may vary between trees
written by a single author and definitely vary between trees written by
different authors, making it just a bit harder to understand a tree written by
someone else.

I think that standardizing the way in which trees are written would help users
understand what each other have written and would also save a lot of time spent
writing boilerplate. This would also help users experiment with different ideas
for tree algorithms more quickly.

### Why a language?

I think that this problem could be solved with an internal DSL.

The DSL could provide a standardized way to specify the information being
stored in the tree and the way algorithms which manipulate the structure of the
tree or perform computations on it should work. Language seems like the natural
way to do this standardization.

A DSL would also have the ability to take most of the boilerplate out of the
hands of the users, much in the say way that ScalaTest dramatically reduces the
amount of code that needs to be written to do unit testing.

One might reasonably suggest that creating some sort of abstract class which
can be subclassed would be sufficient to solve this problem. The core of this
observation is the question of whether such an implementation is really
creating an internal DSL. I claim that it is. The result of people using such a
super-class would be people writing different trees that all use a common
vocabulary inherited from the super-class. I don't think this is the only way
to solve the problem, but even if this was the solution I think it could be
considered a DSL.

### Why you?

I find binary trees to be exceptionally interesting (dare I say magical?)
data structures, and have spent a reasonable amount of time writing different
types of trees in different ways. I think it would be really cool to have a
standardized way of writing tree algorithms that gives you a whole bunch of
debugging information and analysis tools right off the bat.

### Domain

Rapid Binary Tree Development

### Interface (syntax)

I imagine that one could do stuff vaguely like this:

```
Type T

Node Contents:
    data: T

Node Procedure Insert(item: T):
    if item < this.data:
        if this.left exists:
            this.left.Insert(item)
        else:
            this.left = new Node(item)
    if item > this.data:
        if this.right exists:
            this.right.Insert(item)
        else:
            this.right = new Node(item)

Tree Procedure Insert(item: T):
    root.Insert(item)

Tree Procedure Trolololol():
    root.rotateRight()
    root.rotateLeft()
```

The specific symbols used are not particularly important, but the idea is that
standard binary tree ideas (left and right children, node contents, ordered
types) are referred to in a standardize way.

One could also provide a Node MetaData feature which allowed the programmer
to specify metadata associated with each node along with how to compute that
metadata in terms of related parts of the tree. From this the language could
cause that data to be updated only when necessary.

### Operation (semantics)

Just to be clear, this type of DSL would not always be run on its own. I
imagine that the most common case would be that someone uses it to write a tree
and then uses that tree like normal in the host language. The tree would then
behave as if the user had written the entire tree from scratch in the host
language.

Sometimes the user might want to interact with the tree using a visual or CLI
interface for the purpose of debugging or understanding the behavior of the
tree. In this case there would be some sort of host language call provided by
the DSL which would start the visual of command line interface.

Error reporting is an interesting topic. I see three options:
   1. Errors are delayed until runtime (the host language is Python or
      something like that). I see this approach as being very problematic, as
      runtime errors which happen because of user written code may often end up
      surfacing during execution of DSL-internal code confounding the user.
   2. Errors are detected at compile-time by the compiler of the host language.
      I think option is better, as the error would be clearly located in the
      code written by the user. That being said, the error may appear to the
      compiler as a type error or something like that when it is really an
      error related to some tree concept and would ideally reported as such.
      An example of this would be assigning the wrong type to a node's data
      item - the compiler would throw a type mismatch, but a more intelligent
      static analysis tool could say that your nodes don't store X.
   3. Errors are detecting before compilation using a custom static analysis
      tool. This would be a great option too. Users have to use an extra tool,
      but you could detect really complex things. Type mismatches could be
      easily interpreted. You could detect the dependencies of metadata
      computation methods and determine procedure ordering needed to
      recalculate metadata.
I think the second and third are both good options and some thought would have
to go into which one to pursue. The third would require more work and a more
customized build process, but could be very rewarding.

### Expressiveness

I think it should be really easy to do typical tree things - refer to children,
parents, write recursive procedure, etc. It should also be really easy to
understand the algorithms that other have written.

I don't think there should be a lot of things that should be too hard to do. I
imagine that it should be hard to do really tricky stuff like storing extra
information in the least significant bits of child pointers should seem
relatively off limits, but not a lot else.

As an internal DSL, its tough to draw the line between the tree framework and
the host language. Presumably the host language is a general purpose
programming language which gives the users access to all sorts of crazy things,
and they should still be able to use _most_ of those within the tree framework.

### Related work

I don't know of any collected efforts to tackle this problem all at once. That
being said there are some cool bits of code floating around the web that might
serve as good inspiration.

The first of these is some code which prints out binary trees in ASCII. You can
find it
[here](https://datastructuresblog.wordpress.com/2007/12/21/printing-binary-trees-in-ascii/)
. It produces output like:

```
     4
    / \
   2   6
  /   / \
 1   5   7
```

It seems like this would be a nice feature to have in any command line
interface for exploring a tree.

Another thing that comes to mind is the visual binary tree explorer written
originally by Arsen Gogeshvili and enhanced by Prof. O'Neill, found
[here](https://www.cs.hmc.edu/~oneill/BST-Applet/avltree.html). It allows you
look took at how Red Black and AVL trees work, step by step. One could imagine
the visual debugging/exploration interface looking a lot like this.

## The Project
This section examines whether the idea makes for a good CS 111 project.


### Suitability

I think this would actually a reasonable project for DSLs. Most of the time
would be spent trying to figure out how to fit all the tree ideas (in
particular metadata, metadata-yielding procedures, and meta-data dependencies
inside the host language. That being said, implementation could also end up
sucking up a lot of time, so it is hard to say for sure.

I think extensions like the visual and/or command line explorer would be pretty
fun features, but may not be as important or interesting from a DSL perspective
(although the command line explorer would need its own control DSL!).

### Scope

I think this project would be well scoped, partly because of the scope of the
features I've mentioned so far, but also because it has a variable scope. It
would be really easy to say, "Hey , that CLI for tree exploring was a cool
idea, but it's just too much work - we won't do it." Similarly, it'd be easy to
say, "Hey, that CLI explorer control system seems like a good opportunity for a
DSL - let's do that after all because we have the extra time."

### Benefits and drawbacks

I think this is a pretty cool opportunity to explore an internal DSL and think
about how to weave the internal DSL and the host language seemlessly together.
I also think that the metadata dependency problem is sort of cool and it would
be fun to design a DSL which allows the users to express the necessary input to
that problem in a way that feels natural.

I also think that the variable scope would be a really excellent perk from a
class project perspective - it would be easy to scale the project to the amount
of time implementation ends up taking.

Unfortunately I think that in the end of the day not too many people actually
care about this problem. Think about it, who writes different types of trees?
One one side you have people writing them to get certain performance
characteristics, and those people might be more interested in doing
optimizations specific to their type of tree more than they value a
generalizable framework and tool chain. On the other side you have people who
are learning about different types of trees, and learning a DSL just to do that
may not be worth it to them.

I would be super excited about this, but I may be the only person :frown:.
