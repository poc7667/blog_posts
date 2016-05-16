---
title: exception handling practice - extract exception block
date: 2016-04-15 23:09:04
tags: ruby
---

# Ruby better exception handling

We need to clean the raw string and fetch some crudential toks.

However, the similar operations will scatters in differenct children scripts.

Put begin-exception in each `get_locations` method is so annoying.

We could try to extract the begin-exception block into the common function `parse_matches`

# Before

child_a.rb

    def get_locations(line)
      begin
          get_modifier(line)[1].split("/").last.split
      rescue Exception => e
          []
      end
    end

    def get_modifier(line)
      parse_matches(line.scan(/(\[)(.*?)(\])/))
    end

child_b.rb

    def get_locations(line)
      begin
          get_modifier(line)[2].split("/").first.split
      rescue Exception => e
          []
      end
    end

    def get_modifier(line)
      parse_matches(line.scan(/(\[)(.*?)(\])/))
    end

parent.rb

    def parse_matches(matchers, &block)
      rtn = (matchers) ? matchers.first : []
    end


# After


child_a.rb

    def get_locations(line)
        get_modifier(line)[1].split("/").last.split
    end

    def get_modifier(line)
      parse_matches(line.scan(/(\[.*?\])/)) do |rtn|
        rtn[0].split("/")[1].split
      end
    end

child_b.rb

    def get_locations(line)
      get_modifier(line)[2].split("/").first.split
    end

    def get_modifier(line)
      parse_matches(line.scan(/(\[.*?\])/)) do |rtn|
        rtn[0].split("/")[1].split
      end
    end


    def parse_matches(matchers, &block)
      rtn = (matchers) ? matchers.first : []
      begin
        block.call(rtn)
      rescue Exception => e
        []
      end
    end
