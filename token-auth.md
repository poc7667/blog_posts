---
title: Devise Token Auth
tags: rails, angular
---


Only `email confirmation` feature tested for this tutorial,

In this tutorial we will validate the model `Admin` rather than the most common model `User`.

if gem `devise` not installel yet
> rails g devise:install

Add auth for model `Admin` (make sure the model `Admin` has been created, otherwise the following generated migration table will make some troubles.)
> rails g devise_token_auth:install Admin admin_auth

# Gemfile

    gem 'devise', '4.0.0'
    gem 'devise_token_auth', '0.1.37'

# Application controller (disable CSRF on JSON query)

    class ApplicationController < ActionController::Base
      include DeviseTokenAuth::Concerns::SetUserByToken
      protect_from_forgery with: :null_session, if: Proc.new { |c| c.request.format.json? }  
    end

# model/admin.rb (in this case, I don't need email cofirm after registering, So I take off it)

    class Admin < ActiveRecord::Base
      # Include default devise modules.
      devise :database_authenticatable, :registerable,
              :recoverable, :rememberable, :trackable, :validatable,
              :omniauthable
      include DeviseTokenAuth::Concerns::User
    end


# Angular configuration (please refer to the route.rb)

    app.config(function($authProvider) {
        $authProvider.configure({
            apiUrl: '/api/v1/',
            tokenValidationPath: '/admin_auth/validate_token',
            signOutUrl: '/admin_auth/sign_out',
            ...
            Please refer to the official documentation for the following setting
    });

# route.rb

      namespace :api do
        namespace :v1, defaults: {format: 'json'} do
          mount_devise_token_auth_for 'Admin', at: 'admin_auth'
        end
      end


Ref: https://github.com/lynndylanhurley/devise_token_auth#using-multiple-models