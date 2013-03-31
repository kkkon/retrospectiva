source 'https://rubygems.org'

gem "rails", "2.3.15", :require => false
gem "will_paginate", "~> 2.3.0"
gem "acts-as-taggable-on", "~> 2.0.0" 
gem "RedCloth", "4.2.9", :require => "redcloth"
gem 'i18n', "~> 0.4.0"

database = begin
  File.read(File.dirname(__FILE__) + '/config/database.yml').scan(/production.+?adapter\W+(\w+)/im).join
rescue
  nil
end

platforms :mri, :mingw do
  group :postgresql do
    gem 'pg'
  end

  group :sqlite do
    gem 'sqlite3'
  end
end

platforms :mri_18, :mingw_18 do
  group :mysql do
    gem "mysql", "~> 2.8.1"
  end
end

platforms :mri_19, :mingw_19 do
  group :mysql do
    gem "mysql2", "~> 0.2.7"
  end
end

platforms :jruby do
  gem "jruby-openssl", "0.7"

  group :mysql do
    gem "activerecord-jdbcmysql-adapter"
  end

  group :postgresql do
    gem "activerecord-jdbcpostgresql-adapter"
  end

  group :sqlite do
    gem "activerecord-jdbcsqlite3-adapter"
  end
end

group :test do
  gem "rspec", "~> 1.3.0", :require => "spec"
  gem "rspec-rails", "~> 1.3.0", :require => "spec"
  gem "shoulda"
end

local_gemfile = File.join(File.dirname(__FILE__), "Gemfile.local")
if File.exists?(local_gemfile)
  puts "Loading Gemfile.local ..." if $DEBUG # `ruby -d` or `bundle -v`
  instance_eval File.read(local_gemfile)
end

# Load plugins' Gemfiles
Dir.glob File.expand_path("../vendor/plugins/*/Gemfile", __FILE__) do |file|
  puts "Loading #{file} ..." if $DEBUG # `ruby -d` or `bundle -v`
  instance_eval File.read(file)
end
