---
layout: post
title: "Meetup April 11th, 2018"
date: 2018-04-11 21:00:00 -0500
comments: true
categories: [James Bush, Ben Cochran]
---

### Ben Cochran - Pry - A Ruby Developer's Friend
<iframe width="100%" height="300" src="https://www.youtube.com/embed/96OkAtDaBbg" frameborder="0" allowfullscreen></iframe>

In the Ruby world, Pry is IRB on steroids. In a blazingly short period of time you will learn how to install and invoke it, replace your Rails console with it, use it to debug server issues inline, configure macros and shortcuts, and a couple of other neat tips and tricks.

Ben is a Polyglot Principal Full Stack Developer and Architect with 15 years of experience developing standalone and web based applications in Enterprise, Freelance and Startup environments. His company, enhasa.io, is seeking contract work and potential CTO-for-hire engagements. He also has a penchant for 3D Printing as well as using Kubernetes for orchestration of containerized applications.


### [James Bush](https://www.linkedin.com/in/jamesbvsh/) - Generating Markdown Docs for Rails Models with James Bush

James shows off a practical solution to crawl a typical Rails app to generate documentation on models, fields and relationships and output to Markdown.

Video is not available, but here's the code shown in the talk:
```ruby
Rails.application.eager_load!

models_to_document = ApplicationRecord.descendants
  .map(&:to_s)
  .uniq
  .select { |m|
    ActiveRecord::Base.connection.table_exists? m.underscore.pluralize
  }
  .map(&:constantize)

model_descriptions ||= {}

models_to_document.each do |model|
  model_referenced_by = models_to_document
    .select { |m| m.column_names.include?("#{ model.table_name.singularize }_id") }
    .map(&:to_s)
    .join(', ')

  model_references_to = model
    .column_names
    .select { |cn| cn =~ /_id/ }
    .map { |r| r.gsub(/_id/, '') }
    .map(&:camelize)
    .join(', ')

  model_ancestors = model.ancestors.select { |k| k < ApplicationRecord }

  model_descendants = model.descendants

  model_heirarchy = (model_ancestors + model_descendants).map(&:to_s)

  model_column_names = model.column_names.reject { |cn| cn =~ /\Aid|created_at|updated_at|uuid/ }

  model_description = model_descriptions[model.to_s]

  puts "### #{ model.to_s }"
  puts
  print obj "```"
  "#{ model_heirarchy.each { |model_name| puts model_name } }" if model_heirarchy.length > 1
  puts
  puts "#{ model.to_s } <- #{ model_referenced_by }" if model_referenced_by.present?
  puts "#{ model.to_s } -> #{ model_references_to }" if model_references)_to.present?
  puts
  model_column_names.each { |cn| puts "  |#{ cn }" }
  puts "```"
  puts
  puts "#{ model.description }"
  puts
end
```

## Output as Markdown (for a few models):
### User
```
User <- Certification, Invitation, Message, Philosophy, Prep, Resource

  |email
  |encrypted_password
  |reset_password_token
  |reset_password_sent_at
  |sign_in_count
  |current_sign_in_at
  |last_sign_in_ip
  |name
  |gender
  |age
  |bio
  |height
  |phone_number
  |avatar_file_name
  |avatar_content_type
  |avatar_file_size
  |coach
```

### Contest
```
Contest -> Prep

  |title
  |prep_id
  |date
  |url
```

### Conversation
```
Conversation <- Message
Conversation -> Sender, Recipient

  |sender_id
  |recipient_id
```
