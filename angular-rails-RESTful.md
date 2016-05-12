---
title: Angular Rails RESTful
tags: anguar, rails
---


![This post is inspired by this post](https://www.google.com.tw/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&ved=0ahUKEwirs9_m4JnMAhWFGpQKHXiMCJkQFggcMAA&url=https%3A%2F%2Fblog.joshsoftware.com%2F2014%2F11%2F18%2Fhow-to-create-nested-form-using-angularjs%2F&usg=AFQjCNH_5JwCAnpEl8oQ8KTw9VizRrG7Cg&sig2=itfFBS_iY3jnd2U1ZxNr3Q) 


# Prepare `ngRoute`, `ngResource` services

    var myApp = angular.module('myapplication', ['ngRoute', 'ngResource']); 

    //Factory
    myApp.factory('Users', ['$resource',function($resource){
      return $resource('/users.json', {},{
        query: { method: 'GET', isArray: true },
        create: { method: 'POST' }
      })
    }]);

    myApp.factory('User', ['$resource', function($resource){
      return $resource('/users/:id.json', {}, {
        show: { method: 'GET' },
        update: { method: 'PUT', params: {id: '@id'} },
        delete: { method: 'DELETE', params: {id: '@id'} }
      });
    }]);


# CRUD: create a User


#  TIPS

- FORM 裡面的 element 通常都會跟著 form name 名稱做連動 'userForm'
利用 _destroy 屬性 去刪除

## Handle nested params in Rails

The raw params would look like this way

    {"user"=>
      {"addresses"=>
        [{"street1"=>"台灣新北市", "street2"=>"", "city"=>"", "state"=>"", "country"=>"", "zipcode"=>""},
         {"street1"=>
           " 台南",
          "street2"=>"",
          "city"=>"",
          "state"=>"",
          "country"=>"",
          "zipcode"=>""}]},
        "action"=>"create",
        "controller"=>"users",
        "format"=>"json"}

Clean the __user_params__ in controller

      def user_params
        unless params["user"]["addresses"].blank?
          params["user"]["addresses_attributes"] = params["user"]["addresses"]
          params["user"].delete("addresses")
        end
        params.fetch(:user, {}).permit(:first_name, :last_name, :email, :phone,
                                       :addresses_attributes => [:id, :street1, :street2, :city, :state, :country, :zipcode, :_destroy, :user_id])
      end


## User model

accepts_nested_attributes_for is useful 

    class User < ActiveRecord::Base
      has_many :addresses, :dependent => :destroy
      accepts_nested_attributes_for :addresses, allow_destroy: true, reject_if: :all_blank
      def as_json(options={})
        super(:include => [:addresses])
      end
    end
