---
title: add-spring-guard-to-rails-app
date: 2015-12-13 19:14:27
tags: Rails
---

open up `Gemfile`, add these gems

    group :development do
      gem 'guard-rspec'
      gem 'spring-commands-rspec'
      gem 'spring'
    end

install guard for rspec `guard init rspec`

about [sprint server](https://github.com/rails/spring) 

run guard service, `rails g`

