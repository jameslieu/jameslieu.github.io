---
layout: post
title:  "Dropping and resetting database all in one rake task"
date:   2014-07-30 11:41:30
categories: ruby
comments: true
---

When building a new Rails app, I've found that I constantly have had to drop the database, create it, run a migration and finally the seed.

<!--more-->

{% highlight ruby %}
rake db:drop
rake db:create
rake db:migrate
rake db:seed

#=> And for the test environment
RAILS_ENV=test rake db:drop
RAILS_ENV=test rake db:create
RAILS_ENV=test rake db:migrate
RAILS_ENV=test rake db:seed

{% endhighlight %}

This as you can tell can be very tedious. It got me thinking 'What if there was a way to do all of that in one command'. Turns out there is, one way to do it is to create a rake task to run them one after the other.

You can name your task what ever you like:
{% highlight ruby %}
#=> /lib/tasks/db.rake

namespace :db do
  task :rebuild => :environment do
    raise "Cannot run this task in #{Rails.env}"
      unless ['development', 'test'].include? Rails.env

    puts Rake::Task["db:drop"].invoke
    puts Rake::Task["db:create"].invoke
    puts Rake::Task["db:migrate"].invoke
    puts Rake::Task["db:seed"].invoke if Rails.env == 'development'
  end
end
{% endhighlight %}

<br />
With this all you have to do is run the following rake command:
<br />
`NOTE: it goes without saying, NEVER use this in production!`
{% highlight ruby %}
rake db:rebuild

RAILS_ENV=test rake db:rebuild
{% endhighlight %}
And there you have it, a single rake task for both test and development which drops the database, recreates it again, runs a migration and finally the seeds. Be sure not to use this in production because it will drop any data you have in your database.
