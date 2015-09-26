# Free project 2

LaTeX: Once more with feeling!

## The user and a language
This section describes who the project would serve and why a language might be a
good way to meet their needs.


### What's the need?
_What need is met by your idea? Who are you helping? What is that person's
experience like now? What would their experience be like if you could help 
them?_

The users I have have in mind are the users of latex who find it's syntax
somewhat obtrusive. Right now, when people use LaTeX they need to type a lot of
things, and sometimes the semantics are not fully clear.

For example, to use an environment you have to do:

```
\begin{center}
  <stuff to center>
\end{center}
```

Notably many LaTeX users end up indenting the contents of an environment
even though the language doesn't require it. Even those that choose not to
agree that doing so make the code more readable.

I would expand/restrict LaTeX to make it a whitespace sensitive language, which
is just as full-featured as the original, but requires less typing and ties the
layout of the code to the way that code is interpreted.

### Why a language?
_Why is a DSL appropriate for your user(s)? How does it address the need?_

I see the problem as one involving the way users interface with the typesetting
system, not as a problem with the typesetting system itself. By this I mean
that while most people think LaTeX allows them to format things how they
desire, this required syntax is often verbose and cumbersome.

I think that a language is thus the perfect solution to this problem. Making a
language is fundamentally about changing the way two entities interact.

I think the particular problems that a language could solve are:
   1. Making communication between the user and the computer more efficient
      that (less typeing)
   2. Aligning the way users tend to format their code (indentation blocks)
      with the meaning of that code.

### Why you?
_What excites you about this idea? How did you come up with it?_

Almost everyone I talk to has opinions about LaTeX. Those who don't use it note
the complexity of the syntax and the complexity of the build system. Those who
do use it are excited about the typesetting power it provides to them. Those
who use it a lot often complain about the verbosity of the code and the
relative difficulty of finding bugs given the simplicity of the grammar of the
language.

I to use LaTeX, and between my own complaints and the complaints of my peers I
would be excited to improve it in some way.

### Domain
_Describe the project's domain in five words._

Typesetting for power users.

### Interface (syntax)
_How might the user interact with the language? What does programming look 
like? Why is this the right way to interact with the problem domain?_ 

I imagine a syntax in which environments, macro definitions, and one-arguments
macros use whitespace sensitive syntax, something like python:

```
documentclass: article
macro math(string):
    \(string\)
macro equation(string):
    \[string\]
document:
    title: Template
    author: Alex Ozdemir
    \maketitle
    section(My Section):
        paragraph(Why change LaTeX):
            lorem ipsum ...
            equation:
                F=ma

```

I like this syntactic idea because it creates a tight link between how we
format our code and how the output is formatted. I think that the rise of
Markdown has shown that that connection between code form and output form is an
appealing idea
### Operation (semantics)
_What might happen when a program runs? How does a program interact with the
user? What kinds of errors might occur, and how might they be communicated to
the user?_

When a program is compiled the extended syntax would be translated into LaTeX
syntax, which could then be formatted into a PDF using the traditional LaTeX
build system.

All of this would be orchestrated by a single command line tool, which could
present the intermediate LaTeX to the users if they asked for it (much the way
gcc can emit assembly if asked).

This could even be embedded in a traditional LaTeX editor, given the
flexibility of their build system commands. Syntax highlighting might also be
possible, although I'm less familiar with how that system works.

### Expressiveness
_What should be easy to do in this language? What should be possible, but
difficult? What should be impossible or very difficult?_

In general I expect it to be much easy to indicate document structure and I
expect the resulting code to be much easier to read.

I don't think the language would do a lot to improve writing equations in
particular. It seems like equations rely heavily on macros with multiple
arguments, and often appear linearly in the output. The first means that
designing a whitespace sensitive syntax that is useful for equations might be
hard. The second means that it may not even be that important - users don't
seem to have a problem with writing equations in a single linear presentation.

### Related work
_Are there any other DSLs in this domain? If not, describe how you know there
aren't and conjecture why not. If so, describe them and provide links. How well 
do they address the need? Are there any particularly admirable qualities of the
language? Are there parts of the language you think could be improved?_

The ecosystem of formatting and typesetting is a rich one. Let's first consider
the giants: [HTML](http://www.w3schools.com/html/) and
[LaTeX](https://www.latex-project.org/).

Each of these languages is complex, verbose, and full-feature. Anything that
you want to format on the web can probably be managed by HTML. It includes
support for multimedia and a host of other features. Its syntax is simple but
results in long code. LaTeX is similar. It has syntax that is equally verbose
but very general. The LaTeX macro system has even been shown to be Turing
complete. Notably both these languages are whitespace insensitive.

Now lets look at others, [Wiki](https://en.wikipedia.org/wiki/Help:Wiki_markup)
and [Markdown](https://daringfireball.net/projects/markdown/). These languages
are whitespace sensitive and aim to be much less verbose. They both choose to
leave out features in order to simplify the language. Between their lack of
features and relative new-ness they sometimes have unclear semantics -
different interpreters interpret them differently to achieve slightly different
goals (think of emoticons in GitHub's Markdown and the way in which each Wiki
is just a little bit different).

I think that Wiki and Markdown end up being much easier to compose, but limit
user options a lot as a result. I think it would be a good idea to try to build
a language which is as full-feature as LaTeX, but leans on whitespace to make
some common patterns much cleaner to express.

## The Project
This section examines whether the idea makes for a good CS 111 project.


### Suitability
_If someone were to work on this project, what percentage of their time would be
spent directly engaging in the **language** aspects of this project (e.g.,
making language design decisions), as opposed to "systems" aspects of the
project (e.g., implementing a complicated semantics that doesn't require a lot
of language design)?_

I think this might actually be a fairly feasible project. It looks like Paul
Dapolito took a crack at it last year, but only targeted problem sets and
memos. I think it would be good to take a more general approach, and that this
would actually make for a very good DSLs project.

I imagine most of the time would be spent learning a lot about the way LaTeX
works and then deciding what parts of it are acceptable to cut out for the sake
of nicer syntax and more readable code (I can see verbatim being problematic).

I imagine that the implementation side would actually end up being very simple;
you would just write some sort of preprocessor which expands the code into
actual LaTeX.

### Scope
_How big an idea is this? How ambitious is this project?_

I think that this project could be varyingly ambitious. Making a whitespace
sensitive version of LaTeX could be very challenging, but I imagine that by
trimming down parts of the language you could make a more feasible project.

### Benefits and drawbacks
_Why might this be a good idea for a project? Why might this not be a good idea 
project?_

LaTeX is widely used and very well established, which I see as both a benefit
and drawback. On the plus side, even small improvements can end up having a big
impact because of the size of the user base. On the downside it is very well
established, so users may be unwilling to switch over. Making it
backwards-compatible would help with this though.

This wouldn't exactly be an internal DSL, but the desire to make it at least
somewhat compatible with LaTeX would make this project similar to creating an
internal DSL. I think this would actually be a very positive experience because
it requires you to think about two programming languages simultaneously, and
try to find a way to weave them together.
