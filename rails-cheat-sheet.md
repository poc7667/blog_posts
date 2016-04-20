---
title: rails-cheat-sheet
date: 2016-04-15 23:09:04
tags: rails
---

- new Model

    rails g model Bank name:string description:text

# Rspec

RSpec examples

    https://github.com/eliotsykes/rspec-rails-examples
    https://gist.github.com/kyletcarlson/6234923
    https://www.anchor.com.au/wp-content/uploads/rspec_cheatsheet_attributed.pdf


Enable should syntax

    config.expect_with :rspec do |c|
      c.syntax = [:should, :expect]
    end

# Migration



## Rollback

    rake db:migrate:status
    rake db:rollback STEP=1

Migration for belong_to and has_many

    rails g model LoanPlan bank:references name:string description:text lowerbound_rate:float upperbound_rate:float payment_fee:float start_date:datetime end_date:datetime min_lease:integer max_lease:integer min_installments:integer max_installments:integer min_loan_amount:float max_loan_amount:float

# Generator

  With namespace
  
    rails g controller Admin::Dashboard index create delete

  Api generator

  

# paperclip

add logo_image to model `Bank`

    rails generate paperclip Bank logo_image


# Factory girls

make mock data to accelerate test performance


# annotate

It will append the fields/asttribute to your model files.

  - rails g annotate:install
  - rake annotate_models

## spec/models/bank_spec.rb

      it "assign bank name" do
        bank = FactoryGirl.create(:bank)
        bank.update_attribute(:name, "ChinaTrust")
        bank.name.should eql("ChinaTrust")
      end

##factories/bank_factory.rb    

    FactoryGirl.define do
      factory :bank do
      end
    end