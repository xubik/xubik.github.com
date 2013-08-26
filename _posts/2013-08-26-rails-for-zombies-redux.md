---
layout: post
tagline: Notes taken on rails for zombies redux course
---
{% include JB/setup %}

Reference: <http://railsforzombies.org/>

## Level 1: Deep in the CRUD
Rails uses an ORM system to persist objects to a database and allow CRUD operations on this objects.
If a class is called e.g. `Tweet`, then the corresponding database table will be called `tweets`. Ids will be taken care of by the rails framework.

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

Update an attribute and resave, or use `t.attributes` to assign a hash with the updates and then save.

	t = Tweet.find(3)
	t.attributes = {:status => "I really <3 brains", :zombie => "EyeballChomper"}
	t.save

Finally use the `update_attributes` method to automatically save.

### Delete

Delete objects using the method `destroy` on individual objects, or `destroy_all` to obliterate all at once.

	Tweet.find(2).destroy
	Tweet.destroy_all
	
## Level 2: Models taste like chicken
### Models
Before using the model Tweet the class needs to be defined. This is saved in `app/modesl/tweet.rb` and defines a class which inherits from `ActiveRecord::Base` which maps the record to the table.

	class Tweet < ActiveRecord::Base
		validates_presence_of :status
	end
	
### Validation
To make fields mandatory use `validates_presence_of`.  
Lots of other validators are availble to validate the model before allowing persistence to the database.

Alternative syntax for Rails 3 allows validations to be combined on a single line:

	validates :status, :presence => true
	validates :status, :length => { :minimum => 3}
	validates :status, :presence => true, :length => { :minimum => 3}

### Associations
To express associations between objects e.g. between `Tweet`s and `Zombie`s there are the keywords `belongs_to` and `has_many` :

	class Tweet < ActiveRecord::Base
		belongs_to :zombie # note - this is singular
	end

	class Zombie < ActiveRecord::Base
		has_many :tweets
	end
	
To save a new tweet, retrieve the required zombie and then use create, passing in this zombie.

	z = Zombie.find(3)
	t = Tweet.create(:status => "Your eyelids taste like bacon", :zombie => z)

## Level 3: The views ain't always pretty

The Ruby application stack has 4 components, Models on the bottom and Views second from the top.
Rails applications are organised by folder:

* app
	* views
		* layouts
			* application.html.erb # main layout
		* zombies
		* tweets
			* index.html.erb # lists all tweets
			* show.html.erb # views one tweet
	* models 
* public
	* stylesheets
	* javascripts
	* images

`.erb` stands for Embedded Ruby

### Tags used in html files

`<% %>` to evaluate Ruby  
`<%= %>` to evaluate Ruby and print the result  
To indicate where to add the main content in the template file use `<%=yield%>`  

### Additional layout components

`<%= stylesheet_link_tag :all %>` will write out the appropriate html to include all stylesheets in the public/stylesheets directory  
`<%= javascript_include_tag :defaults %>` will inlude all the default javascript (jquery from Rails 3.1)
`<%= csrf_meta_tag %>` cross site request forgery meta tag will add meta tags to the top of the doc and other tags to forms

### Root path and images

When a resource is requested by the browser it will automatically be searched for in the `public` folder first. If not found, the request will be sent to Rails.

### Adding a link

To add a link use `<%= link_to [link text] [link path url] %>`  
So to link to the page for that zombie use e.g. `<%= link_to tweet.zombie.name zombie_path(tweet.zombie) %>`  
This can alternatively be written  `<%= link_to [link text] [object to show] %>`  
e.g. `<%= link_to tweet.zombie.name tweet.zombie %>`  

### Checking builtin methods

There are many options you can use with the method `link_to`.
In order to find more information about this method:

1. Git clone the rails code and use grep to search for that method name: `grep -r 'def link_to'`
2. Use the online documentation at api.rubyonrails.org
3. 
