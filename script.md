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













