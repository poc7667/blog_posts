---
title: SUBURI setting on Rails with Nginx
---

# ENV

- ENV['RAILS_RELATIVE_URL_ROOT']=/browse/

# routes.rb

    scope ENV['RAILS_RELATIVE_URL_ROOT'] do
        get 'browse/category_detail'
        get '*path' => redirect('/')
    end


# application.rb

      class Application < Rails::Application
        config.relative_url_root = ENV['RAILS_RELATIVE_URL_ROOT']
      end


# Error in production log

    I, [2015-10-20T07:07:15.956058 #30522]  INFO -- : Started GET "/" for 127.0.0.1 at 2015-10-20 07:07:15 +0000
    F, [2015-10-20T07:07:15.957575 #30522] FATAL -- :
    ActionController::RoutingError (No route matches [GET] "/"):

# nginx.conf

    server {
            listen 443;
            server_name WEBSITE.COM;
        location /browse {
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header Host $http_host;
            proxy_redirect off;
            proxy_pass http://unix:/tmp/puma.broswe.sock:/;
        }
    }%