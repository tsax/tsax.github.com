---
layout: post
title: "Redirect_to and preservation of errors"
date: 2013-03-25 00:38
comments: true
categories: [pecunia-nunc, debugging, side-projects]
---

Working on my side project, [Pecunia-Nunc](https://github.com/tsax/pecunia-nunc/), I was baffled when the errors on the object creation form would not display upon submission. The controller looked like this

{% codeblock lang:ruby%}
class SubscribersController < ApplicationController

def new
	require 'digest'
	@subscriber = Subscriber.new(params[:subscriber])
	@subscriber.token = Digest::SHA1.hexdigest([Time.now, rand].join)
	if @subscriber.save
		flash[:notice] = "Thanks for signing-up. Please confirm your email address through the email that'll be in your inbox shortly!"

		redirect_to home_path
	else
		flash[:notice] = "There were errors! Please resubmit after making corrections."
		redirect_to home_path
	end	
end
...
{% endcodeblock %}

The view :
{% codeblock lang:ruby%}
  <% if @subscriber.errors.any? %>
  <div id="error_explanation">
    <div class="alert alert-error">
      The form contains <%= pluralize(@subscriber.errors.count, "error") %>.
    </div>
    <ul>
    <% @subscriber.errors.full_messages.each do |msg| %>
      <li>* <%= msg %></li>
    <% end %>
    </ul>
  </div>
<% end %>
{% endcodeblock %}

As you can tell, the problem was not in the view at all, but in this line ```redirect_to home_path```. Redirection clears the object.errors field, and therefore nothing was being displayed. I stupidly spent a lot of time fiddling with the view, instead of inspecting the controller action. Replacing the problematic line with ```render 'new'``` ('new' is the action/view that renders the form) solved the problem by preserving the .errors object.
