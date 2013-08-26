---
layout: post
tagline: Notes taken on rails for zombies course
---
{% include JB/setup %}

Reference: <http://railsforzombies.org/>

## Level 1: Deep in the CRUD
Rails uses an ORM system to persist objects to a database and allow CRUD operations on this objects.
If an class is called e.g. `Tweet`, then the corresponding database table will be called `tweets`. Ids will be taken care of by the rails framework.

### Create

Create a new object and call `save` to persist it to the database.

	t = Tweet.new
	t.status = "I <3 brains"
	t.zombie = "Jim"
	t.save
	
Alternatively, create the new object using a hash:

	t = Tweet.new(:status => "I <3 brains", :zombie => "Jim")
	t.save
	
Or all in one line using create
	
	Tweet.create(:status => "I <3 brains", :zombie => "Jim")
	
### Read

There are lots of ways to read information from the database:

	Tweet.find(2)			# find by id
	Tweet.find(3,4,5)	# return multiple objects
	Tweet.first			# returns the first tweet
	Tweet.last
	Tweet.all
	Tweet.count			# returns the result of a select count(*) on the database
	Tweet.order(:zombie)	# return the tweets ordered by :zombie
	Tweet.limit(10)		# just 10 tweets
	Tweet.where(:zombie = "Ash")
	Tweet.where(:zombie = "Ash").order(:zombie).limit(10)
	
### Update

