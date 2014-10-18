# Matz

Slide 1

Hello, my name is Yukihiro Matsumoto, also known as Matz. Thank you for coming to RubyConf 2003, it's nice to see a bigger crowd this year! In our first year in 2001, we only had 33 or so, and last year, maybe 50.

Slide 2

Why are we here? We are here because Ruby is Good Enough for many of our tasks. So we do not have to talk about that.

Slide 3

So I am going to talk about How Ruby Sucks and how we can make it better.

Slide 4

Ruby has these problems - for example, it's slow and inconsistent. How can we fix these?

Slide 5

With a major version change from 1.0 to 2.0, this is the opportunity to take one big step and make changes that may not be backwards compatible, but will make Ruby better. To clarify, Ruby 2 is the next version of the Ruby language, and Rite is the virtual machine for Ruby 2.

Slide 8

The path we will take to Ruby 2 depends on being free of 1.8 maintenance. Hopefully that will be soon. Then in 1.9, we will work on the syntax changes. I do not know what those changes will be yet, but there will be experiments.

Once we know what the syntax will be, then we can work on the implementation in Rite.

Rite will be vaporware for a long time, unfortunately. I am still waiting for a Son-Shi to finish Rite for me!

Slide 9

So here are some things that we might experiment with for Ruby 2.

Slide 26

For example, here is a way we could have keyword arguments. Here, `a` is positional and the `b` argument is a keyword argument and the order does not matter. You must use the keyword argument name, in this case `b`, if you specify it, if not it will be some kind of error but I have not decided what kind of error yet.

Slide 27

This is a new hash literal syntax that we might have, that would be equivalent to the current syntax we have.

Slide 28

Maybe we could have method hooks that would let you add code to arbitrary methods to be run before or after. `def` *may* return an object, I'm not sure yet. If you try to add a pre method to a method that does not exist, that would throw an error. Or maybe not.

Slide 32

As you can see, I am undecided about many of these changes. I would like help from you in the form of Ruby Change Requests for a time, until about March 2004. These would be proposals asking if we could change Ruby in this way or that way. RCRs should contain an abstract, motivation, proposal and rationale. They can be big changes that would not be backwards compatible. I think I will reject most of them, but thinking about how to make Ruby better by many brains is better than just one small brain.

# DHH

Here we go. So I hope you can read the text, the first thing we do is called the rails command... to generate the skeleton of the application. See, so, it generated a bunch of things, a bunch of files, and then the next step, the very next step? is starting the ruby server. So seeing that everything works. The only prerequisite to this is that you have ruby on rails installed.

Whoops! It worked! We are up and running. We have the web server running, and it's saying it worked.

And now, let's create the first thing. We're going to create the controller that's gonna run this blog. So we have this "script generate controller" which is like a macro for creating these things. So now we have a blog controller and we're going to see if that works.

Whoops! We didn't have any actions in there, usually, so we're going to create the index action. The index action is the first action, you see the mapping that we're going to do. And we're just going to say "Hello world". And we're going to reload, and Hello World! That's how much work you have to do to get to "Hello world"! That's not a lot. So this was just saying "hello world" from within the controller, not very interesting. Normally we want the nice model view controller split so now we create a template.

Look at all the things I'm *not* doing. Look at all the configuration I'm *not* writing. All these things are mapped together just automatically. Just by saying blog up here maps directly to the blogging controller and just by having index maps directly to the index template. Hello from the template. And now we even remove the action and show that it could go all the way to the template without having an action.

All right. Next thing. Setting it up with a database-- that's the only piece of configuration you really need to do because, unfortunately, rails can't read your mind yet. So it doesn't know your password. Thankfully. So we create the first database, we're going to call it blog development, and we're going to create the first table. So a blog should have posts, right? So posts, in plural. We create the table, just having an id, by default all these model tables just have an ID, and we're just going to start out simple, just with a title. So all these posts are just going to have a title by now. And i am going to create the model. i just created the table for it but i dont have an object for it yet, but now i also created the post model. so you see over here, it's just an empty one again, but just having that already gives it a ton of capability because it descended from the active record thing.

So now we're going to use something called scaffold. Scaffold is a quick way of putting your module--Whoops! we need to restart the server when we change the database configuration. so, let's just do that. Um, scaffolding is a way of easily putting a model object online in a way that you can edit it. Whoops! We didn't create this, this was created for us just by the scaffolding thing. Now we're going to create a new post, just... "hello brazil". Yaaay! Post was successfully created.

# _why

To code in ruby is really to love. It stirs you inside. When I walk down the street and look into people's eyes I can see their excitement about learning rails. Y'know? I can see that they know David Hennemeier Hanson, that they want to be him, they want his fine apparel, and his ways, y'know. There's a rushing out in the streets to get here. And that's pretty cool. It seems like this is the sort of thing we need to start administering to our children, for their health. It's the sort of thing that you... just... really can't be whole without, y'know?

So one of the ways that I've been messing with ruby is with cartoons and stuff. And there's a science behind this. This is incredibly thought out. And, i mean, wow, foxes, y'know, of all animals. These are the foxes that I use in the book I'm working on, and it's sort of a reactionary work to try and do something that a technical book *shouldn't* do.

The eyes of the foxes. Round and blank. There's nothing there, right? What do you have to hold onto in a technical book, y'know? What drives you to read it, exactly? Is there a personality there? Is there feeling, is there humanism, is there humanity in a technical manual? Not really, there shouldn't be. The eyes should be blank. They should be staring straight ahead, poring through pages and pages. Reference material. You gotta get this down. You cannot blink. That's the foxes, they never blink in the book. And that's an allegory. Of you! If they stare, you stare back! It helps keep you focused.

(on the short one)

This is the one I like. Cause you can't ever see anything about him. He's always down there at the bottom. And that's supposed to be sort of frustrating. I know I don't have incredible things to teach in the book, I'm not an incredible programmer or anything like that, but I figure people will keep reading to see a little bit more of the short one, because maybe there's something down there.

19:00 - double splat

19:45 - not worth your $500

20:00 - matz is super cool, unruffled, matz is nice

22:30 - creator is biggest weakness? whaa?

# Tenderlove

O-M-G! O-M-G! Happy Thursday everybody! Welcome to Ruby Conf Ten! I love that it's ruby conf X because i think of it as the extreme ruby conf.

I have to put this slide in because every time I give a talk I'm actually very nervous up here, and a friend of mine told me, when you're on stage, just think about "What would freddie mercury do?" So I put this up here to remind myself to think about that and calm down.

So today we're going to look at some tips and tricks for improving the performance in your ruby code by looking at things I used to improve the performance of ARel.

So how did I get started with this? There's a feature I've wanted to add to Rails for a very long time, and that is prepared statement caching, and we'll actually have that feature in Rails 3 point 1. In order to add this to active record, a deeper understanding was required of active record. So I started diving in and fixing bugs, going through the lighthouse ticket tracker and fixing bugs in active record. And I ran across one that said active record is five times slower than in rails 2.3.5. This was before rails 3 was released and you can go read up on the ticket here. And I thought to myself, five times slower? really? five times slower? how is that possible? and it *is* possible! It really was five times slower! So I thought that I'd look into this, and I thought, what could possibly go wrong?

So, motivation. Why do we care about speed? We all know that ruby can't scale, and rails can't scale, and yet, we're all rubyists, right?

As a tangent, I've discovered the technique for scaling ruby. and it goes like this. it's very simple, like this. Look at that scale. It scales very beautifully. Now, the thing is, the difference between ruby and java is that when you scale java, it doesn't pixellate like this.

But I'm asking you all why you want to make your code faster, and really, I'm just trolling you. Usually, the slow code is linked to poor code, so if we identify bits that are slow, we can find bad code in our system and get rid of it.

When should I make my code faster? Easy answer to this. When it isn't fast enough. But then the question is "What is fast enough?" Whenever I think about this, I think, well, do people notice it? and what are you comparing it to? In my mind, fast enough means that it finishes in a reasonable amount of time and that is subjective.

And really, I'm telling you all these things but I don't want you to believe me. I want you to think critically and go out and look at this stuff and analyze it for yourself.

For performance, we need to reduce method calls, branching and looping, and we need to reduce objects. What I think is interesting is that, for clean code, the things to reduce are exact

So the things we need to minimize for minimizing our use of time and space are exactly the things we need to minimize for clean code, so therefore, clean code equals performant code.

So conclusion, aka the things I've learned: System impact. It looks like this, and right there in the middle is a very depressing time. I learned: When should I rewrite? I see it like this: the earliest you should rewrite is when Ryan Davis says so, and the latest you should rewrite is when I say so you should probably pick a time in between there.

We emphasize the art of code, but we should not forget the science.

# Corey

So how many of you do TDD? How many of you, when you run your tests, sit there and wait, 10, 20, 30 seconds-- admittedly, it gives you time to be witty on twitter... but, if you think about it, if you wait 20 seconds each time you run your tests in the TDD red-green-refactor cycle, that's about 100 seconds for code that took you 1 second to write.

Wouldn't it be nicer if your tests looked like this?

I want to talk about why we are at this point. Why we have these test suites that are so long. And I want to go back to the beginning. So years ago, we were introduced to Rails, to the idea of MVC on the web, we were learning about it, we watched the 10 minute blog video, we thought "Awesome, I can do that." Rails *came* with something that was an *amazing* step forward for us. It came with a test folder. It said you should be writing automated tests.

So as we're learning how to do MVC on the web, and we start talking about fat models and skinny controllers. And people talk about how we really should be putting business logic in our models-- the wonderful thing is that while we're experimenting with design and learning how to do rails applications, we can run our tests.

Today, we've started seeing large codebases that are causing test suites to take 15 minutes, an hour. A lot of it boils down to the difference between Test First and Test Driven Development.

The rails test suite, as wonderful as the testing paradigm was there, there was a fundamental disconnect in that they weren't a test suite designed to do test-driven development, they were a test suite designed to do test-first development.

In my definition, it's all about how you react to the pain of tests. In test-first dev, you change your tests. So you might build things like spork or specjour, which alleviate the pain in testing by altering the way your tests run. But they're just band-aids. In test-driven, when you have pain, you change your *design*. That's the *point* of test-driven development.

So let's talk about the underwhelming part of this-- some techniques for doing this. The key is to take what we already know. So we isolate ourselves from 3rd party APIs, it's a standard design technique, and then we let our tests get like this. So ask yourselves why your tests take 20 seconds to start up-- and there's one culprit, rails. So why not take the idea of isolation, and go one step further. What's the biggest 3rd party thing that I'm dependent on? Rails!

# Sandi

1:43 - i'm here today to tell your future :)

25:30 - your fortune

27:45 - first programming job

31:00 - still morning in our community

33:15 - habitat for humanity's volunteer mgmt software sucks

34:30 - wind at our backs

# Jim

# Jeremy and Carol







