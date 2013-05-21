---
layout: post
title: "I'm Not a Spammer"
date: 2013-04-09 02:05
comments: true
categories: [side-projects, pecunia-nunc, ruby, learning]
---
For my current side-project, I need to send emails to a list of people whose email addresses are stored in the database. My concern, as you can imagine, is to prevent spamming my users in instances of error or otherwise. There's several ways to do this. As usual, it comes down to a choice - a judgement call from among the many choices. 

1. Creating an emails model to keep track of when an email was sent and to whom.
2. Storing the last time a user received an email in the user model.

You can think of many others ways to do this of course.
I decided to go with the second option as it required minimal effort and has so far turned out
very well. This was accomplished with a single ```rails generate migration AddLastEmailToSubscribers last_email:datetime```.

This will create the following migration
``` ruby AddLastEmailToSubscribers
class AddLastEmailToSubscribers < ActiveRecord::Migration
  def change
    add_column :subscribers, :last_email, :datetime
  end
end

```
