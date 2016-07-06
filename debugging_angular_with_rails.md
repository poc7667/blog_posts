---
title: gulp
date: 2016-04-09 10:14:42
tags: javascript
---

![inline](https://i.imgur.com/EAh2GMN.png=300x "Title")

 "PATH_INFO"=>"/portal/run@http://10.0.0.44:3000/portal/index.html",
 "REMOTE_ADDR"=>"10.0.0.42",
 "puma.socket"=>#<TCPSocket:fd 15>,
 "rack.hijack?"=>true,
 "rack.hijack"=>#<Puma::Client:0x3fd47df7c984 @ready=true>,
 "rack.input"=>#<Puma::NullIO:0x007fa9005aa608>,
 "rack.url_scheme"=>"http",
 "rack.after_reply"=>[],
 "ORIGINAL_FULLPATH"=>"/portal/run@http://10.0.0.44:3000/portal/index.html",

UNEXPECTED_PATH_PREFIX = "/portal/run@"
if  UNEXPECTED_PATH_PREFIX in env["PATH_INFO"]
    env["PATH_INFO"].gsub!(UNEXPECTED_PATH_PREFIX,"")
end
 "PATH_INFO"

  "ORIGINAL_FULLPATH"=>"/portal/run@http://10.0.0.44:3000/portal/index.html",



    def call(env)
    host = env["HTTP_HOST"]
    # ["PATH_INFO", "ORIGINAL_FULLPATH", "REQUEST_URI"].each do |item|
    ["REQUEST_PATH", "REQUEST_URI", "ORIGINAL_FULLPATH", "PATH_INFO"].each do |item|
      if env[item].include? host
        start_of_pos = env[item].rindex(host)+host.length
        env[item] = env[item][start_of_pos..-1]
        if env[item].end_with? "/portal/index.html"
          env[item]="/"
        end
      end
    end

    ["REQUEST_PATH", "REQUEST_URI",
      "HTTP_REFERER","SERVER_NAME", "SERVER_PORT",
      "ORIGINAL_FULLPATH", "PATH_INFO"].each do |k|
        ap("#{k}:#{env[k]}")
    end

    ap(env)
    # binding.pry if env["REQUEST_PATH"].include? "/portal/index.html"

    @status, @headers, @response = @app.call(env)
    [@status, @headers, @response]
  end