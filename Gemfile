source 'https://rubygems.org'

# Uncomment the database that you have configured in config/database.yml
# ----------------------------------------------------------------------
gem 'mysql2', '0.3.10'
# gem 'sqlite3'
# gem 'pg', '~> 0.13.2'

# Allows easy switching between locally developed gems, and gems installed from rubygems.org
# See README for more info at: https://github.com/ndbroadbent/bundler_local_development
#gem 'bundler_local_development', :group => :development, :require => false
#begin
#  require 'bundler_local_development'
#  Bundler.development_gems = [/^ffcrm_/, /ransack/]
#rescue LoadError
#end

# Removes a gem dependency
def remove(name)
  @dependencies.reject! {|d| d.name == name }
end

# Replaces an existing gem dependency (e.g. from gemspec) with an alternate source.
def gem(name, *args)
  remove(name)
  super
end

# Bundler no longer treats runtime dependencies as base dependencies.
# The following code restores this behaviour.
# (See https://github.com/carlhuda/bundler/issues/1041)
spec = Bundler.load_gemspec(Dir["./{,*}.gemspec"].first)
spec.runtime_dependencies.each do |dep|
  gem dep.name, *(dep.requirement.as_list)
end

# Remove premailer auto-require
gem 'premailer', :require => false

# Remove fat_free_crm dependency, to stop it from being auto-required too early.
remove 'fat_free_crm'

gem 'unicorn'

group :development do
  gem 'thin'
  gem 'quiet_assets'
  gem 'capistrano'
  gem 'capistrano_colors'

  # Use zeus and guard gems to speed up development
  # Run 'zeus start' and 'bundle exec guard' to get going
  unless ENV["CI"]
    gem 'guard'
    gem 'guard-rspec'
    gem 'guard-rails'
    gem 'rb-inotify', :require => false
    gem 'rb-fsevent', :require => false
    gem 'rb-fchange', :require => false
  end
end

group :development, :test do
  gem 'rspec-rails'
  gem 'headless'
  gem 'debugger' unless ENV["CI"]
  gem 'pry-rails' unless ENV["CI"]
end

group :test do
  gem 'capybara'
  gem 'selenium-webdriver'
  gem 'database_cleaner'
  gem "acts_as_fu", "~> 0.0.8"

#  if RUBY_VERSION.to_f >= 1.9
    gem 'factory_girl_rails', '~> 3.0.0'
#  else
#    gem 'factory_girl_rails', '~> 1.7.0'
#  end
  gem 'factory_girl_rails'
  gem 'zeus' unless ENV["CI"]
  gem 'coveralls', :require => false
end

group :heroku do
  gem 'unicorn', :platform => :ruby
  gem 'pg', '~> 0.13.2'
end

gem 'memcache-client'
gem 'newrelic_rpm'

# Gems used only for assets and not required
# in production environments by default.
group :assets do
  gem 'sass-rails',   '~> 3.2.3'
  gem 'coffee-rails', '~> 3.2.1'
  gem 'uglifier',     '>= 1.0.3'
  gem 'execjs'
## We use node
#  unless ENV["CI"]
#    gem 'therubyracer', :platform => :ruby
#  end
end

gem 'turbo-sprockets-rails3'
