# frozen_string_literal: true

source 'https://rubygems.org'

ruby '2.4.10'

gem 'rails', '5.1.0'
gem 'sqlite3'

gem 'jbuilder', '~> 2.0'
# bundle exec rake doc:rails generates the API under doc/api.
gem 'sdoc', '~> 0.4.0', group: :doc

gem 'acts-as-taggable-on', git: 'https://github.com/mbleigh/acts-as-taggable-on'
gem 'acts_as_follower'
gem 'devise', '~> 4.2'
gem 'jwt', '~> 1.5.4'
gem 'puma'
gem 'rack-cors', '~> 1.0.5'

# ActiveModel has_secure_password
# gem 'bcrypt', '~> 3.1.7'

# Unicorn for the app server
# gem 'unicorn'

# Capistrano deployment
# gem 'capistrano-rails', group: :development

group :development, :test do
  # Call 'byebug' anywhere in the code to stop execution and get a debugger console
  gem 'byebug'
  gem 'listen'
end

group :development do
  # Speed up development by keeping your application running in the background. Read more: https://github.com/rails/spring
  gem 'pry'
  gem 'rubocop', require: false
  gem 'spring'
end
