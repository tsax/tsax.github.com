---
layout: post
title: "pow environment variable trouble"
date: 2013-02-15 01:57
comments: true
categories: [pow, environment-variables, bugs, rails, projects]
---
I was caught up in excitement upon discovering [pow](http://pow.cx). After setting it up, and testing it out on the project I'm working on now, I encountered a problem. My app is setup to send email using Gmail thru SMTP configured in a Rails environment config, and the email is sent using ActionMailer. 

The config looks like this
``` 
    address: "smtp.gmail.com",
    port: 587,
    user_name: ENV["GMAIL_USERNAME"],
    password: ENV["GMAIL_PASSWORD"],
    authentication: :login

```

  The emails were arriving when I tested the app by running ```rails server``` but on the local pow server, authentication errors were the norm. Clearly the environment variables weren't being set. So I googled pow's documentation for how to setup environment variables, ending up on [this page](http://pow.cx/manual.html#section_2.2). While reading through the linked section, I missed something critical. 

  "Pow attempts to execute two scripts — first .powrc, then .powenv — **in the application's root**. Any environment variables exported from these scripts are passed along to Rack."

  So I idiotically set about creating a .powrc file in my user/bin directory. Obviously this did not work, but I wasted an hour or so tweaking random settings trying to get this to work. Then I re-read the page, set about to fix the problem, which I did as follows.

  1. Run ```touch .powrc``` in my project's root.
  2. Edit .powrc and add the environment variables as follows:
  ```
  export GMAIL_USERNAME=username
  export GMAIL_PASSWORD="my password"
  ```
  3. Restart pow's worker for the app by running 
  ```touch tmp/restart.txt```

  And that worked!
