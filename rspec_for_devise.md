Take note for preparing Rspec test for devise


# rails_helper.rb

require 'support/request_helper'
require 'devise'
Dir[Rails.root.join("spec/support/**/*.rb")].each { |f| require f }

RSpec.configure do |config|
  # Remove this line if you're not using ActiveRecord or ActiveRecord fixtures
  config.fixture_path = "#{::Rails.root}/spec/fixtures"
  config.include Devise::TestHelpers, :type => :controller
  config.extend ControllerMacros, :type => :controller
  ...