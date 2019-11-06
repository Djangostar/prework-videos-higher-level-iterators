# Higher Level Iterators

## Learning Goals
+ Identify some common manipulations for lists of data
+ Use each to iterate over a list of items and do something with it
+ Use map/collect to create a list of new values
+ Use select to return a filtered list of values
+ Explain how to find other Enumerable methods in ruby

## Lesson
<iframe width="100%" height="720" src="https://www.youtube.com/embed/lvGr9Y6KQrE?rel=0&showinfo=0" frameborder="0" allowfullscreen></iframe>

+ Hi folks, it's Ian from Flatiron School. In this video, we're going to look at some higher level iterators in Ruby. Our learning goals for this video - by the end of this video, you should be able to:
  + Identify some common manipulations for lists of data
  + Use each to iterate over a list of items and do something with it
  + Use map/collect to create a list of new values
  + Use select to return a filtered list of values
  + Explain how to find other Enumerable methods in ruby
+ So let's go ahead and get started.
+ In programming, we often deal with lists of data. One of the powerful things about code is that you can process long lists of data in a repeatable way.
+ Let's pretend that we have an array with hashes representing people
  + Each one has a name, email, and height (in inches)
+ Here's a list I generated using Faker. Faker is a library for creating fake data - this is not required, but I'll leave a link to it in case you feel like playing around with it
```ruby
people = [
  {:name=>"Dr. Garrett Effertz", :email=>"nevillerunolfsdottir@leschbradtke.com", :height=>64},
  {:name=>"Marci Johnson", :email=>"dee@wilkinson.co", :height=>64},
  {:name=>"Corrin Kertzmann", :email=>"nelson@schimmellang.org", :height=>59},
  {:name=>"Mr. Mel Parisian", :email=>"alanestark@runolfon.io", :height=>63},
  {:name=>"Dale Schowalter", :email=>"raguelgerhold@ziemannschaden.info", :height=>60},
  {:name=>"Lakita Hills", :email=>"claudko@yostbatz.net", :height=>67},
  {:name=>"Chasity Schowalter", :email=>"jerrica@barrows.org", :height=>59},
  {:name=>"Carmen Sipes PhD", :email=>"joaquinstiedemann@durgan.io", :height=>83},
  {:name=>"Mrs. Lonnie Jacobs", :email=>"domenicwiegand@osinski.com", :height=>74},
  {:name=>"Shanon Corwin", :email=>"lanell@sengerstanton.name", :height=>65}
]
```
+ How might print out each person's email address?
+ One way to do this is using the .each method - so people.each do person, and then I'll write end.
+ And in the block, this code will run once for each person we have, so I can just write `puts person[:email]`
```ruby
people.each do |person|
  puts person[:email]
end
```
+ That's great - .each is a great method when we want to do something to each item in our list of users.
+ Right now, we're just printing this to our console. But you could imagine, if we had a method that could send an email, we could also use this to email each person. Just imagine that we have this method called `send_email_to` that can take in this hash, and that method would magically know how to send a nice email to this person.
```ruby
people.each do |person|
   send_email_to(person)
end
```
+ So, you have to imagine that we have that method, but this is something that we could definitely do using each. .each is a great method when we want to do something with each element.
+ Say, though, that we want to manipulate the data first. So let's pretend that I need an array of just email addresses - maybe I want to give that list to someone, and I want them to have the emails but not the other data for some reason.
+ How might I transform this list of hashes into a list of just email addresses?
+ One way would be to make a new array, and then iterate over the people using the each method, and for each person I could shovel the email address into the new array.
```ruby
def email_addresses(people)
  email_addresses = []
  people.each do |person|
    email_addresses << person[:email]
  end
  email_addresses
end
```
+ So, in this example, we have to create a data structure, then add each email to it, then return that data structure again.
+ So we end up with a bit of a sandwich here - where the variable `email_addresses` is the bread on top and bottom, and then the manipulation is in the middle.
+ Anytime we see this, this is a bit of a code smell - this gives me a clue that there's a better way to do this.
+ In Ruby, we can use a method called `map`
+ Map works similarly to `.each` in that you call it on an array, and it takes a block.
+ Instead of just doing something on each element though, map will actually create a new array based on whatever the block returns.
+ So here's kind of a weird example:
```ruby
people.map do |person|
  "Hi!"
end
```
+ Each time through, our block returns "Hi!". So this code will actually return an array with the word "Hi!" in it ten times.
+ One thing about `map` - it always returns an array with the same number of elements
+ The cool thing is, we have access to the value on each pass through the iteration. So instead of returning the same thing, we can return some value based on the iteration. For example, if we had an array of numbers, we could return an array of the numbers doubled.
```ruby
doubled = [0, 1, 2].map {|number| number * 2 } # [0, 2, 4]
```
+ For our person example, we can use map to take the email address out for each person.
```ruby
people.map do |person|
  person[:email]
end
```
+ So this is helpful for getting that new array of email addresses. I like the name `map` for this method, because we're mapping a value to a new value. Ruby actually aliases this as `collect` - this does the same thing, so it's up to you which one to use. Some people like collect because they feel like they're collecting a bunch of new values.

+ Now, sometimes, we actually want to trim our list down. For example, let's say we want to find everyone who's under 6 feet tall. Same as our first example, we could do this using `.each`, a new array, and a conditional
```ruby
def under_six_feet(people)
  under_six_feet = []
  people.each do |person|
    if person[:height] < 72
      under_six_feet << person
    end
  end
  under_six_feet
end
```
+  So this works, but we have that code smell again, we see this sandwich. So there must be another way. And luckily, Ruby has another built-in enumerator called `.select` This method takes a true/false statement in the block, and will make a new array with anything that returns true.
+ In this case, our true/false statement is right here - `person[:height] < 72` - if that's true, we want this value in the new array
+ So I'm going to change this to use select, and then I can get rid of everything else besides that true/false statement in the block
```ruby
def under_six_feet(people)
  people.select do |person|
    person[:height] < 72
  end
end
```
+ So this code does exactly the same thing as before - it's just a little bit more expressive and shorter to read.
+ You as the programmer know - ok, they're using select here, so they're filtering down the values. You don't have to read all the details about it.
+ Really the goal here is to just make our code as expressive as possible, and this really expresses an idea.
+ So using the correct iterator is really helpful for that.
+ There are way too many iterators to demonstrate in one video, but I'll do a quick recap of a few others
+ .find is similar to select, but it will return to you a single object, whichever one meets the condition first. So this is good if you think you only have one thing that meets the condition - for example, if I'm searching by email address or something like that
+ sort_by let's you sort by a specific condition, so I could sort this list either by height or by email address
+ inject is great if you want to get a new value. So maybe I want to know the total height in inches of everybody, I can inject 0 into this list and then add the height to it each times
+ Again, those are a just a few. There are tons of these that you can look up, I'll link to the documentation here that I'm browsing to that you can check them out.
+ That's it for this video - just to recap:
  + We identify some common manipulations for lists of data - doing something with data, getting a new array, filtering or sorting the list
  + We used the .each method to iterate over a list of items and do something with it
  + We used the map/collect method to create a list of new values
  + We used  the select to return a filtered list of values
  + And we talked about how to find other Enumerable methods in Ruby, such as find, sort_by, inject, and many more
+ Thanks for watching - happy coding!
