# Higher Level Iterators

## Learning Goals
+ Identify some common manipulations for lists of data
+ Describe the process for iterating over collections of data
+ Use each to iterate over a list of items and do something with it
+ Use map/collect to create a list of new values
+ Use select to return a filtered list of values
+ Use find to return the first value matching a condition
+ Use sort_by to sort the list by a certain value
+ Explain how to find other Enumerable methods in ruby

## Outline
+ In programming, we often deal with lists of data. We often want to manipulate that data and do some changes.
+ Say that we have an array with hashes representing people
  + Each one has a name, email, and height (in inches)
  + NOTE:: feel free to pair this list down if it makes sense
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
+ How might we write a method that takes that prints out each person's email address?
```ruby
people.each do |person|
  puts person[:email]
end
```
+ That's great - .each is a great method when we want to do something to each item in our list of users. This could be
  + Print/display data
  + send an email to each person or call some other external service
+ Sometimes, we want to manipulate that data first. So, maybe I want to transform this list of hashes into a list of just email addresses How might I do that?
+ One way would be to make a new array, use each, and then return the array
```ruby
def email_addresses(people)
  email_addresses = []
  people.each do |person|
    email_addresses << person[:email]
  end
  email_addresses
end
```
+ Point out how, in this example, we have to create a data structure, add the email to it, then return in
+ Anytime we see this, this is a bit of a code smell - this gives me a clue that there's a better way to do this.
+ In Ruby, we can use a method called `map` -> map will return a new array based on the return value of the block
```ruby
people.map do |person|
  "Hi!"
end
```
+ This will return an array with "Hi!" in it 10 times. `map` always returns an array with the same number of elements
+ Each time, we can change this to be the email address of the person
```ruby
people.map do |person|
  person[:email]
end
```
+ So this is helpful for getting that new array of email addresses.

+ Repeat with filtering with `select` - filter out anyone over 72 inches tall 
+ Show documentation for find and sort
