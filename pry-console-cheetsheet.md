---
title: pry-console-cheetsheet
date: 2016-04-27 17:18:34
tags: ROR
---

# edit .pryrc

enable tabular format on query

add these to `.pryrc`

    require 'hirb'
    Hirb.enable
    Pry.config.print = proc do |output, value|
      Hirb::View.view_or_page_output(value) || Pry::DEFAULT_PRINT.call(output, value)
    end
