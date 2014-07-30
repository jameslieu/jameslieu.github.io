---
layout: post
title:  "Tired of your dropping database and restarting it over again?"
date:   2014-07-30 11:41:30
categories: ruby rails
---

When building a new Rails app, I've found that I constantly have had to drop the database, create it, run a migration and finally the seed.

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


This as you can tell can be very tedious. A better solution I've found is to create a rake task to handle it all.


{% highlight ruby %}
#=> /lib/tasks/db.rake

namespace :db do
  task :rebuild => :environment do
    raise "Cannot run this task in #{Rails.env}" unless ['development', 'test'].include? Rails.env
    puts Rake::Task["db:drop"].invoke
    puts Rake::Task["db:create"].invoke
    puts Rake::Task["db:migrate"].invoke
    puts Rake::Task["db:seed"].invoke if Rails.env == 'development'
  end
end
{% endhighlight %}

With this all you have to do is run the following rake command:

{% highlight ruby %}
rake db:rebuild
RAILS_ENV=test rake db:rebuild
{% endhighlight %}

`NOTE: it goes without saying, NEVER use this in production!`
