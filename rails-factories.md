---
title: factories
date: 2016-07-06 23:09:04
tags: rails
---

用來快速產生 mock 資料的好幫手，讓測試更加easy.

An easy way to populate mock data on testing.

<!-- more --> 


# spec/factories/rooms.rb

    FactoryGirl.define do
      factory :room_type do
        name "DEFAULT_ROOM_TYPE"
        english_name "MyText"
        factory :single_room do
            name "單人房"
            guests 1
        end
        factory :twin_room do
            name "雙人房"
            guests 2
        end
        factory :semi_double_room do
            name "雙人房"
            guests 2
        end
        factory :quad_room do
            name "四人房"
            guests 4
        end
      end
    end


# spec/fixture/hotel_fixtures.rb

    RSpec.shared_context :build_room_type do
      before(:each) do
        FG.create(:single_room)
        FG.create(:twin_room)
        FG.create(:semi_double_room)
        FG.create(:quad_room)
      end
      after(:each) do
        RoomType.destroy_all
      end
    end



## spec/models/room_spec.rb

It will create room_type records for you on

    RSpec.describe Room, type: :model do
      include_context :build_room_type    
      ...    