---
title:  "Single Table Inheritance in Rails"
date:   2022-01-24 12:00:00 +0000
tags: rails oo db
author: Trevor Vallender
---

Yesterday I implemented Single Table Inheritance in a Rails app I'm working on.
Here, I want to document the process. I'm using Rails 7 but this should be
applicable to most recent versions.

Single table inheritance is a method of organising object-oriented data in a
relational database. Instead of having individual tables for every class in your
application, you store multiple classes of an object in one table which has a
"type" column to store what class of object that row should create. For example,
in my note-taking application, a Todo is a subclass of Note, but both are stored
in the notes table.

This is most useful when dealing with very similar classes which only diverge in
small ways, otherwise we end up with very large amounts of null data in the
table and don't really gain anything.

My main two classes are *Note* and *Todo*, with *Todo* a subclass of *Note*.

# The type column

First we need a type column on the table, which is then used to determine the type of object a database row represents. We should disallow null values here, and optionally supply a default. This gave me:

{% highlight ruby %}
class AddTypeToNote < ActiveRecord::Migration[7.0]
  def change
    add_column :notes, :type, :string, default: 'Note', null: false

    add_index :notes, :type
  end
end
{% endhighlight %}

In order to automatically set the type of a new object, I then added the
following:

{% highlight ruby %}
class Note < ApplicationRecord
  ...
  after_initialize :set_defaults

  def set_defaults
    self.type ||= 'Note'
  end
end
{% endhighlight %}

Now *type* will be automatically set, even prior to being written into the
database.

You can quite happily continue using controllers as normal, but I wished to use
the *Notes* controller to handle most requests for both classes — everything
except *index*. So our routes file looks like this:

{% highlight ruby %}
Rails.application.routes.draw do
  ...
  resources :notes, only: [:index, :show, :new, :create, :update]
  resources :todos, only: [:index]
  resources :todos, only: [:update, :show, :new, :create], controller: 'notes', type: 'Note'
end
{% endhighlight %}

Obviously if you're continuing to use individual controllers for each class type
you don't need to do this.

In my application I have a form which can create and edit both *Notes* and
*Todos*. This can lead to the form getting confused if it's passed one when it
expected the other. One way to deal with this is using *Persistence#becomes*,
which returns an instance of the class you specify with the attributes of the
current record. Its primary use is just what we're doing here — having a
subclass appear as its superclass. Here it is in action:

{% highlight erb %}
<%= form_with model: @note.becomes(Note) do |f| %>
...
<% end %>
{% endhighlight %}

And there we have it! Fairly simple stuff, although you should think carefully
about whether this is the right data structure for your application as it can be
more brittle and less easy to change than the more traditional approaches.
