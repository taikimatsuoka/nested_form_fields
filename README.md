# Nested Form Fields

This gem helps creating forms for models with nested has_many associations.

It uses jQuery to dynamically add and remove nested associations.

- Works for arbitrarily deeply nested associations (tested up to 4 levels).
- Works with form builders like simple_form.
- Requires Ruby 1.9 and the Rails asset pipeline



## Installation

Add this line to your application's Gemfile:

    gem 'nested_form_fields'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install nested_form_fields
    
In your application.js file add: 

    //= require nested_form_fields

## Usage

Assume you have a user model with nested videos:

    class User < ActiveRecord::Base
      attr_accessible :name, :videos_attributes
      has_many :videos
      accepts_nested_attributes_for :videos, allow_destroy: true
    end 

Use the *nested_fields_for* helper inside your user form to add the video fields:

    = form_for @user do |f|
      = f.nested_fields_for :videos do |ff|
        = ff.text_field :video_title
        ..
  
Links to add and remove fields can be added using the *add_nested_fields_link* and *remove_nested_fields_link* helpers:

    = form_for @user do |f|
      = f.nested_fields_for :videos do |ff|
        = ff.remove_nested_fields_link
        = ff.text_field :video_title
        ..
      = f.add_nested_fields_link :videos
      
Note that *remove_nested_fields_link* needs to be called within the *nested_fields_for* call and *add_nested_fields_link* outside of it via the parent builder.


## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Added some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request