# Matz

Slide 1

Hello, my name is Yukihiro Matsumoto. Thank you for coming to RubyConf 2003, it's nice to see a bigger crowd this year-- about 45 people!

Slide 2

Why are we here? We are here because Ruby is Good Enough for many of our tasks. So we do not have to talk about that.

Slide 3

So I am going to talk about How Ruby Sucks and how we can make it better.

Slide 4

[...summarize bullet points]

Slide 5

[...mention what Rite is, that Ruby2 will have breaking changes, that need to be free of 1.8 maintenance first. do not know what the changes will be yet, have a lot of ideas]

Slide 24

[...here is something i am considering]

Slide 26

[...keyword arguments]

Slide 27

[...hash syntax]

Slide 28

[...method hooks]

Slide 29

[...seletor namespace]


Slide 32

I would like help from you in the form of Ruby Change Requests for a time, until about March 2004. These would be proposals asking if we could change Ruby in this way or that way. RCRs should contain an abstract, motivation, proposal and rationale. They can be big changes that would not be backwards compatible.

[fade out]

# DHH

Here we go. So I hope you can read the text, the first thing we do is called the rails command... to generate the skeleton of the application. See, so, it generated a bunch of things, a bunch of files, and then the next step, the very next step? is starting the ruby server. So seeing that everything works. The only prerequisite to this is that you have ruby on rails installed.

Whoops! It worked! We are up and running. We have the web server running, and it's saying it worked.

And now, let's create the first thing. We're going to create the controller that's gonna run this blog. So we have this "script generate controller" which is like a macro for creating these things. So now we have a blog controller and we're going to see if that works.

Whoops! We didn't have any actions in there, usually, so we're going to create the index action. The index action is the first action, you see the mapping that we're going to do. And we're just going to say "Hello world". And we're going to reload, and Hello World! That's how much work you have to do to get to "Hello world"! That's not a lot. So this was just saying "hello world" from within the controller, not very interesting. Normally we want the nice model view controller split so now we create a template.

Look at all the things I'm *not* doing. Look at all the configuration I'm *not* writing. All these things are mapped together just automatically. Just by saying blog up here maps directly to the blogging controller and just by having index maps directly to the index template. Hello from the template. And now we even remove the action and show that it could go all the way to the template without having an action.

All right. Next thing. Setting it up with a database-- that's the only piece of configuration you really need to do because, unfortunately, rails can't read your mind yet. So it doesn't know your password. Thankfully. So we create the first database, we're going to call it blog development, and we're going to create the first table. So a blog should have posts, right? So posts, in plural. We create the table, just having an id, by default all these model tables just have an ID, and we're just going to start out simple, just with a title. So all these posts are just going to have a title by now. And i am going to create the model. i just created the table for it but i dont have an object for it yet, but now i also created the post model. so you see over here, it's just an empty one again, but just having that already gives it a ton of capability because it descended from the active record thing.

So now we're going to use something called scaffold. Scaffold is a quick way of putting your module--Whoops! we need to restart the server when we change the database configuration. so, let's just do that. Um, scaffolding is a way of easily putting a model object online in a way that you can edit it. Whoops! We didn't create this, this was created for us just by the scaffolding thing. Now we're going to create a new post, just... "hello brazil". Yaaay! Post was successfully created.

# _why

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














