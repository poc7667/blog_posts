---
title: rails-cheat-sheet
date: 2016-04-15 23:09:04
tags: rails
---


# If rb-readlin not working, you can not type double chars in your console , try this


CONFIGURE_OPTS="--disable-install-doc --with-readline-dir=/usr/local/opt/readline" rbenv install 2.3.1




- new Model

    rails g model Bank name:string description:text

# Strong params

Params

    {"product"=>
      {"id"=>9,
       "specs"=>
        [{"type"=>"text", "value"=>"price"},
         {"type"=>"float", "value"=>"description"},
         {"type"=>"text", "value"=>"我好帥"}],
         ...

Whielist SPECS params (JSON format)

    def product_params
      params.require(:product).permit(
        :name,
        :specs => [:type, :value]
      )
    end


# Many to Many

Generate migration, remember the params should be real name of data table

     rails generate migration CreateJoinTableLoanPlanCareer loan_plans careers

JSON API

    json.extract! @loan_plan, :id,
    json.careers @loan_plan.careers do |t|
        json.id t.id
        json.name t.name
        json.description t.description
    end


# Sanitize Nested params

Raw params

     "loan_plan" => {
                      "id" => 32,
                 "careers" => [
            [0] {
                         "id" => 8,
                       "name" => "police officer123434",
                "description" => "Tattooed vinyl jean shorts irony. Iphone wolf kinfolk austin venmo semiotics authentic slow-carb. Farm-to-table poutine letterpress asymmetrical hammock microdosing. 3 wolf moon viral offal portland."
            },
            [1] {
                         "id" => 9,
                       "name" => "engineer",
                "description" => "Wes anderson polaroid jean shorts meggings etsy roof listicle 90's. Tote bag plaid green juice. Microdosing 8-bit austin migas."
            }
        ]
    },

You want to preserve careers with IDs, the syntax is strange, somehow this is the Rails way :(

    def loan_plan_params
      params.require(:loan_plan).permit(
        :id, 
        {:careers=>:id}
      )
    end

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

Add field

    rails generate migration add_specs_to_products specs:json

## Rollback

    rake db:migrate:status
    rake db:rollback STEP=1

Migration for belong_to and has_many

    rails g model LoanPlan bank:references name:string description:text lowerbound_rate:float upperbound_rate:float payment_fee:float start_date:datetime end_date:datetime min_lease:integer max_lease:integer min_installments:integer max_installments:integer min_loan_amount:float max_loan_amount:float

# Generator

With namespace
  
    rails g controller Admin::Dashboard index create delete

Api generator

    rails g model Post title:string body:string
    rake db:migrate
    rails generate scaffold_controller api/Post --model-name=Post

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