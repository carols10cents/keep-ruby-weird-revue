# From Paul Brannan, http://rubystuff.org/rubyconf/notes03.outline

- SUMMARY: Matz gave the keynote address in which he talked about his visions for
  Ruby 1.9 and Ruby 2.0 (Rite).  He talked about the development path
  for Ruby 2.0 and about new features that Ruby 2.0 will have (many oohs
  and aahs came as we saw some of these features).  He also explained
  his desire to see the RCR (Ruby Change Request) process improved.  He
  requested that in the next few months we submit RCRs that may
  change/improve Ruby drastically, but mandated a format that all these
  RCRs must follow (in the past, RCRs have been freeform, resulting in
  requests that are not very well thought out).  At the end of the talk
  we got a quote from Matz in true Matz style: "Coding in Ruby is a joy,
  and coding in C is like a puzzle.  I like puzzles."  Links that may be
  of interest:
    - http://www.rubyist.net/~matz/slides/rc2003/
    - http://www.rubygarden.org/ruby?Rite

- Matz - Visions for the Future (Keynote)
  - Ruby is good enough, but nothing is perfect
  - "How Ruby Sucks"
    - slow
    - complex
    - surprising
    - inconsistent
    - bad embedding
    - no native threading, no M17N
  - Ruby 2 / Rite
    - Slightly incompatible with 1.8, but better syntax
    - Rite - bytecode-based VM
  - Path to Ruby 2
    - After 1.8.1 released, start on 1.9.x
    - 1.9.x: experiment with Ruby2 syntax, M17N features, Onigurama,
      generational GC
    - then, move to Rite
      - the hard way
      - vaporware for a long time
      - Matz needs to clarify syntax, be free from 1.8
    - still waitong for "Son-Shi" (guru) to write VM :)
  - Local variable scopes
    - old behavior: variables created in the block are block-local
    - new behavior:
      - no block-local variables by assignment
      - block parameters always local (even if vars with same name
        already exist)
  - Instance variables
    - @foo - can be accessed from subclass
    - @_foo - local to class/module
    - (or, maybe, other way around)
  - Constant lookup
    - Current: surrounding class, nesting class, base class,
      const_missing to raise error
    - New: superclass, surrounding nesting class (1 level only),
      const_missing
  - Class variables
    - Current: surrounding class, superclass, error
    - New: all class variables local to the class/module
  - Statement and expression
    - "foo" "bar" --> error
    - (long_expression \n + another_long_expression) --> valid
    - (abc; def) --> error
  - Multiple values
    - a,b,c = x (where x = [1, 2, 3])
    - does it produce a=1, b=2, c=3 or a=[1, 2, 3], b=nil, c=nil?
    - (source of confusion)
    - could we raise an exception if arity on left and right don't
      match?
    - div, mod = x.divmod(y) --> should this be an error?
    - Solution
      - separate arrsys and multiple values strictly in syntax -OR-
      - represent multiple values by subclass of Array
      - both have drawbacks, but are better than current behavior (which
        is yield handles multiple values, but return does not)
      - Matz has no concrete idea yet, but says something must be done
    - Ryan Davis believes that consistency is important ("don't mess
      with my objects!"; divmost should return multiple values instead
      of an array)
    - long discussion followed here...
  - Method visibility
    - Now: private/public/protected all in one namespace
    - Perhaps put private into separate namespace (maybe, just an idea)
    - (currently creating method "print" messes up namespace for
      subclasses)
    - Huge incompatibility
  - Range in condition
    - print line if f.lineno == 1 .. f.lineno == 2
    - .. works like awk
    - ... works like sed
    - should be removed or changed; ideas wanted
  - Keyword argument
    - def foo(a, b : 42, **keys); p [a, b, keys]; end
    - a is a positional argument
    - b is a keyword argument (only need colon, not 42)
    - foo(1) #=> [1, 42, {}]
    - foo(2, b:5) #=> [2, 5, {}]
    - foo(3, b:4, c:6) #=> [3, 4, {:c=>6}]
    - foo(1, 2, 3) #=> error? (Matz is undecided)
    - foo(:foo=>1, :bar=>2, b:3) #=> [{:foo=>1, :bar=>2}, 3, {}]
  - New hash literal
    - { a:45, b:55, c:65 } will be equivalent to { a=>45, b=>55, c=>65 }
  - Method combination
    - Hooks can be added to arbitrary methods
      - def foo:pre
        - cannot affect args
      - def foo:post
        - cannot affect return value
      - def foo:wrap
        - calling super in this method calls the original method
        - args and return value can be affected
      - more than one wrap method results in calls being stacked in
        order of definition
      - will def return an object? - Matz is undecided
      - foo:pre but no foo --> error
      - can I call foo:pre directly? - NO!
      - can I wrap all methods in a class? - no.
      - discussion about AOP followed here.
      - does defining foo:pre invoke method_added? - no (maybe call
        pre_added?)
  - Selector namespace
    - define String#to_i ONLY IN THE NAMESPACE
    - reason: global changes to existing classes are evil!
    - Problems
      - hard to implement efficiently
      - hard to understand for traditional OO users
      - may not be needed where RubyBehavior and scope-in-state will do
    - will namespaces be objects? - Matz does not know
    - namespaces will be statically scoped
  - Optional type
    - StrongTyping and types.rb are based on class/module, which hinders
      duct typing
    - need type system based on signature (method signature)
    - needs to be built-in to be efficient
    - no concrete idea yet
  - Request for RCR
    - we need to progress to live
    - big step at once to reduce tragedy
    - proposal: free to make drastic RCR for a while (until March 2004?)
    - following information required: abstract, motivation, proposal,
      rationale
    - these conditions should be met:
      - incompatibility OK, but should not break the "Ruby way"
    - Matz gave sample RCR - obsoleting "proc" (RCR#1)
    - "Designing lang is very fun"
    - Most of these RCRs will be rejected
    - Thinking about making ruby better by many brains is good
  - Things we've already been told
    - bytecode (CISC > RISC for soft VM, indirect branch using GCC
      henhancement; if GCC is available, Ruby runs faster)
    - generational GC - mostly generational, mostly thread-safe
    - M17N
      - handle multiple character codeset at once
      - code-set independent (no code conversion unless explicitly
        specified)
      - handles unicode as well
      - semi-automatic code conversion by IO class
  - Plans for near future
    - 1.9.x
    - RCR - still need time to consider
      - wait for RCRs
    - Rite - will remain vapourware for a while
  - "Coding in ruby is a joy, and coding in C is like a puzzle.  I like
    puzzles."
  - http://www.rubyist.net/~matz/slides/rc2003

# From Ryan Davis, https://web.archive.org/web/20060217000939/http://www.rubygarden.org/ruby?Rite

(Sorry to edit up front, but I want to stress that Matz said "maybe" to nearly every feature he presented during his keynote. It was much more of a brainstorming session than it was a laundry list for Rite. Matz, correct me if I'm wrong. --RyanDavis)

Next generation Ruby === Rite
This is as of now mostly a copy of Matz's slides. Feel free to refactor and expand as needed.

Matz's keynote topic at Rubyconf 2003: "How Ruby Sucks"

The slides of this presentation can be found at: http://www.rubyist.net/~matz/slides/rc2003/

Overview

The new revision of the language will be Ruby 2.0; its implementation will be Rite. Sometimes one term is used to refer to both, but when meaningful Ruby2.0 and Rite will be considered as two separated entities. Both the language and the implementation will change.

The language
Ruby2 will be slightly incompatible, the changes will not only consist of additions but also of syntax improvements (hopefully a better syntax will result).

The implementation
Rite will be a bytecode based, thread-safe virtual machine. Care will be taken to make embedding easier than in 1.x.

The procedure
Matz has planned a precise path that will lead to Ruby2.0 and its implementation, Rite.

After releasing 1.8.1, 1.9 will be started; it will be an experimental release, primarily for language experimentation, but 1.9 won't be "Rite". Ruby 1.9 development starts right after 1.8.1 Final.

What Matz plans to do

    First: clarify Ruby2 syntax
    Second: get out of 1.8 maintenance

Matz is "still waiting for a guru to finish Rite for him". Many fail to see the implications of this... for some background, read RubyTalk:76588 and RubyTalk:76603. The son-shi award is at stake!

Release engineering
Matz wants to

    Maximize breakages as we shift to 2.0
    Minimize them afterwards

This means that 2, 3, 4 versions will contain major changes that could potentially break things. Sub-releases such as 2.x won't.

Ruby 1.9 is essentially going to be 2.0 in terms of syntax but not implementation. Some of the things that will be tested in 1.9 include

    a new regular expressions library: Oniguruma
    a generational GC

Upcoming changes in the language
Ruby 2 will change:

    variable scopes
    the difference between statement and expressions
    semantics of multiple values
    private method visibility
    range in condition
    keyword arguments
    new hash literals

and more.

Variable Scope
Block locals
Local variable scope will be changed. Matz considers them the "most regrettable behavior in Ruby". No "block local" variables by assignment. Block params will be block local, even if the same name variable exists previously, local variables in eval() die after eval, all block params will be local.

Matz stated before that shadowing would cause a warning -- it is unclear in his presentation whether this will be the case in the end or not.

    def foo
        a = nil
        ary.each do |b|
          #b  is block local
          c = b
          a = b
          # a and c are local to the method (i.e. NOT block local)
        end
        # a and c here
    end

Instance variables

It will be possible to make them local to the class/module (so that derived classes won't be able to access them).

    @variable  # can be accessed by subclasses
    @_variable # not accessible by subclasses
               # "or the other way around"

Class variables

@@variables are going to be local to the class/module. You will have to define accessors to get to them from outside.

New constant lookup rules:
The search for constants will happen in the following order:

    up the inheritance chain (superclasses) until Object
    surrounding nesting class (1 level only)
    then call const_missing (Also potentially a big code breaker)

    class Foo
      A = 1
      B = 2
    end
    module Mod
      B = 3
      C = 4
      class Bar<Foo
        p Bar    # => Mod::Bar (rule 2)
        p A      # => 1 (rule 1)
        p B      # => 2 (rule 1)
        p C      # => 4 (rule 2)
        p D      # => error! (rule 3)
      end
    end

Change in semantics on multiple values:

    a, b, c = x
    where x = [1,2,3]
    should they be:
    a=1,b=2,c=3
    or:
    a=[1,2,3],b=nil, c=nil

Matz still hasn't decided, but it will be either:

    Represent multiple values by subclass of Array, say Array::Values<Array

or

    Separating arrays and multiple values strictly in syntax

Method visibility:
"private" may be moved to a separate name space (DEFINITELY maybe) :) so, private methods may not clash with protected/public methods, even if they have the same name. "print" is an example, but this could be a huge incompatibility.

Range in Condition:
This behaves like awk or sed now.

    print line if f.lineno == 1 .. f.lineno == 2

Matz wants to either remove or change it (he says he doesn't even know what that code snippet does ;)

Keyword args:

    def foo(a, b: 42, **keys)
        p [a,b,keys]
    end
    #
    foo(1)           # => [1,42, {}]
    foo(2, b:5)      # => [2,5, {}]
    foo(3, b:4, c:6) # => [3,4,{:c=>6}]

If you don't specify the double star argument, the unspecified keyword would be nil. Order is not important for keyword args; the variable "a" is positional in the previous examples.

Mandatory keywords
When calling a method with keyword arguments, you have to include the varname.

    foo(1,2,3)     # => raises some kind of error
    foo(1,b:2,c:3) # => this is correct
    foo(1,c:3,b:2) # => this too

Matz is not sure yet about the kind of error that should be raised.

New hash literals:

    {a: 45, b: 55, c: 65}

same as:

    {:a => 45, :b => 55, :c => 65}

Hooks
Hooks can be added to arbitrary methods

    class Foo
        def foo:pre(*args)
            p "pre"
        end
        #
        def foo:post(*args)
            p "post"
        end
        #
        def foo:wrap(*args)
            p "wrap pre"
            super
            p "wrap post"
        end
        #
        def foo(*args)
            p "foo"
        end
    end
    #
    Foo.new.foo

gives:

    wrap pre
    pre
    foo
    post
    wrap post

"def" may return an object; doesn't know yet

    class Foo
       def foo:pre(*args)
       end
    end

Throws an error at time of definition, because no foo method exists to "pre" against. But maybe not... Matz may change his mind on that (based on suggestion from audience)

    Foo.new.foo:pre # NOT legal

Selector namespaces

It might be possible to encapsulate changes to classes (redefinition of methods, new methods, etc.) inside an arbitrary scope:

   $a = "4"
   namespace foo # syntax may change
     class String
       def to_i
         0
       end
     end
     p $a.to_i   # => 0, in this namespace
   end # of namespace
   p $a.to_i     # => 4

Some consequences to be expected would be:

    metaprogramming becomes easier and safer because changes to "common" classes can be localized

There are a number of cons:

    it is hard to implement efficiently
    hard to understand for OO users
    may not be needed if libraries (written in Ruby) approximate this behaviour

Optional typing

Matz finds the current typing systems (StrongTyping? and types.rb) based on class/modules are too restrictive and hinder duck typing. He's looking for ideas to implement a system based on method signatures and integrate it in the VM core.

Open questions

    What problem is Matz trying to fix?
        increase speed (might involve dynamic compilation/optimization based on types)
        catch errors earlier (possible to do it shortly after parse-time???)
    To what extent would this change The Ruby Way (according to Matz, it won't, since he wouldn't accept such modifications)

Older news about Rite (the implementation)
These are the things we knew already (from previous presentations or postings in the mailing list)

    Bytecode interpreter
    Generational, conservative (as now) garbage collector: using a mixture of 1 bit reference counting and mark & sweep. It will be (mostly) thread safe
    m17n
    Indirect branch using gcc enhancement (computed gotos)
    Super operators (CISC is better than RISC for software VM)

If GNU gcc is available, it will run faster (because of computed gotos)

    multiple simultaneous character codeset handling (you're not forced to use Unicode, but it will be supported: UTF8, UCS2, etc.)
    semi-automatic code conversion by IO class

The process

RCRs

Philosophy:

    We need to progress to live.
    Make one big step at once to reduce upgrade tragedy.
    Consider thoroughly before making big changes
    We need more brains to think about them... not only one small brain

Free to make drastic RCR for limited time only until March 2004

An RCR should be more than mere "hope". The following information is required:

    abstract
    motivation
    proposal
    rationale

...the following condition should be met:

    incompatibility is ok, as long as it doesn't change "the ruby way"

Matz showed http://www.rubyist.net/~matz/slides/rc2003/mgp00034.html an example of what he expects a RCR to look like, advocating the removal of "proc", so that only "lambda" would remain (to prevent confusion with Proc.new and its different semantics). It is unclear whether he actually plans to carry this out.

The RCR blitz should happen before March/2004. Matz says "I think I will reject most of them" :-) RCRs will not happen on RubyGarden.org going forward. DavidBlack has created a http://rcrchive.net site for RCRs.

Plans for near future
1.9

    oniguruma (new regular expressions library)
    generational GC
    m17n (multilingualization)
    ...other changes :)

Matz still needs time to consider RCRs... will wait for some

Rite will remain vaporware for a while

Questions to clarify

Here are some open questions it would be great if this page could answer:

What about Parrot? Has it anything to do with Rite?
Parrot is Perl6's upcoming virtual machine (http://www.parrotcode.org). It has been designed specifically for Perl but some care has been taken to make it work with other languages (Ruby and Python come to mind). People from the Cardinal project planned to make a compiler targetting Parrot bytecode for Ruby, but the project seems frozen at the moment (no activity in the mailing list for months).

Parrot doesn't affect Matz's plans at all: he will make his own VM (Rite), which will be the reference implementation if Parrot is ever able to run Ruby code and becomes more popular than Rite.

Parrot promises top-notch speed and the ability to share libraries written in several languages; many people remain rather sceptical in that regard. It is widely believed that Matz's independent creation of a VM specific for Ruby could be completed faster and better than Parrot's all-encompassing goal.

-- MauricioFernandez

If you want bytecode and a VM and great garbage collection & threading model
You could experiment layering the Ruby 2 language parser on top of the Groovy (http://groovy.codehaus.org/) AST model (which is a Ruby-like language) which compiles down to Java bytecode and sits snugly on top of the JVM, and has great integration with the Java platform. Then you'd have Ruby language with a VM and bytecode and threading model. Only downside is the C integration might not be as good as if you did your own VM & bytecode.

Just a thought: this could allow you to progress Ruby 2, the language, while a separate team writes a VM, etc.

-- JamesStrachan?

The JavaVM would be unacceptable for a great many of Ruby's users because it is non-free - or to avoid an argument over the meaning of "free", let's say "does not conform to the Open Source Definition." For some languages this might not matter, but for a language like Ruby I would suggest that it does.

The Kaffe VM would then be an option, but there is the same problem with C integration. And I think C integration is just about the most important thing for a scripting language.

But it might be worth evaluating presently-existing free virtual machines out there. The ones I have found so far are: Scheme48, GNU Smalltalk, gforth/vmgen, and LLVM.

What kind of community input will this process have
Read the section about RCRs.

Where does the name Rite come from?

See RubyTalk:96642 http://blade.nagaokaut.ac.jp/cgi-bin/scat.rb/ruby/ruby-talk/96642
Hi,

In message "Where does the name Rite come from?"
    on 04/04/06, Michael Neumann <mneumann / ntecs.de> writes:

|Where does the name Rite come from? rewRite? :-)

The name popped in my mind one day.  I coined Rite as "Ruby that
should be light (both syntax and implementation)" afterwards.

							matz.



# From Jim Weirich https://web.archive.org/web/20031206085208/http://onestepback.org/index.cgi/Tech/Conferences/RubyConf2003/

Visions of the Future - Keynote Address (Yukihiro Matsumoto)

Finally, the moment we’ve all been waiting for, to hear news about Rite and Ruby 2. After an (short) introduction by David Black, Matz begins by saying that Ruby is "Good Enough" and that’s why we are here. So the real topic is "How Ruby Sucks", and what we will be doing about it.

First of all, Matz drew the distinction between what is Ruby 2 and what is Rite. Ruby 2 is the next version of the Ruby language. Matz plans to take advantage of the major version upgrade and introduce some things to clean up the language that are not necessarily backwards compatible. Rite refers specifically to the VM for Ruby 2.

So, with that in mind, here are some things that may by in Ruby 2.

Note:
    The following is a paraphrase of the information Matz provided. The talk generally moved too fast for me to capture all the details, but I tried to capture the overall gist of the topic. If there are any inaccuracies, it is entirely my fault.
Note 2:
    I discovered later that Chad Fowler had logged onto IRC during the keynote talk, and was streaming this same information into the IRC channel. Someone not at the conference was then taking the IRC information and updating the Ruby wiki pages in real time. That’s pretty cool.

    Local Variable scope. Block parameters will be block local, hiding any existing variables. Also, local variables created by "eval" will
    Instance Variables. @_foo will be truely private (not protected). Or maybe @foo will be private and @_foo protected. Matz hasn’t decided yet.
    Constant Lookup. New rule will check enclosing class, then all superclasses, then one level of nesting classes. This simplifies the rules for constant lookup.
    Class Variables. Now class variables will will be local to the class or module. Use accessors if you wish to access class variables from a larger scope.

    Question:
        How will class variables be different from class instance variables?
    Answer:
        Class instance variables are normal instance variables of the class object. Class variables will be more like static variables that are scoped by the class.

    Statements and Expressions. No implicit string concatenation (use "+"). Parenthesis will cause line continuations. Statement grouping by parenthesis will be disallowed, use begin/end instead.
    Multiple Values. Multiple value assignment is confusing. We can either separate arrays and multiple values strictly by syntax. Or we could use a subclass Array::Values < Array to return values. Matz hasn’t decided which solution he will go with. (There was a lot of questions and comments on this item).
    Method Visibilities. Private may be in a separate namespace from public/protected.
    Range in Condition. This is confusing. No one remembers the exact semantics (even Matz)
    Keyword Arguments. Finally! Here’s the scoop:

      def foo(a, b: 42, **keys)
        p [a,b,keys]
      end
      foo(1)               => [1,42,{}]
      foo(2, b: 5)         => [2,5,{}]
      foo(3, b: 4, c: 6)   => [3,4,{:c=>6}]

    Some Smalltalkers wanted an optional colon after foo. Matz said no.
    New Hash Literal. A new form of Hash literal will be available.

      { a: 1, b: 2, c: 3 }  == { :a => 1, :b => 2, :c => 3 }

    Method Combination. Pre, Post and Wrap method combinations will be available. These methods are modelled after the CLOS before/after/around modifiers.

     class Foo
       def foo:pre();  p "pre"; end
       def foo:post(); p "post"; end
       def foo:wrap(); p "wrap pre";   super;   p "wrap post"; end
       def foo();      p ;foo"; end
     end

    prints …

     wrap pre
     pre
     foo
     post
     wrap post

    Selector Namespace. It will be possible to modify the behaviors of selections within statically scoped namespace. Details are subject to change.
    Optional Type. Current strong typing experiments are class/module based. Matz is exploring options, but wants any solution to be signature based and efficient.

Matz is interested hearing about ideas, so he is encouraging RCRs (Ruby Change Requests) for a limited time (say March 2004). He wants more than mere "could we change it this way" type of requests, but RCRs should contain an abstract, motivation, proposal and rationale. Mats demonstrates an "proper" RCR#1 with the proposal to remove "proc" from the language.

After talking about Ruby 2, the language; Matz moved on to talk a bit about Rite, the VM for Ruby 2. Ruby 1.9 will be a testing ground for some items targeted for Rite. It sounds like the big push will be for dealing with M17N. The new RegEx engine (handling M17N) will be in 1.9.

You can find the slides at: www.rubyist.net/~matz/slides/rc2003/
