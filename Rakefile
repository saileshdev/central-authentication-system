ENV["API_ENV"] ||= "development"
require "bundler/gem_tasks"
require "rake/testtask"
require "active_record"

Rake::TestTask.new(:test) do |t|
  t.libs << "test"
  t.libs << "lib"
  t.test_files = FileList['test/**/*_test.rb']
end

namespace :db do
  desc "Creates the tables to work with."
  task :migrate do
    ActiveRecord::Base.establish_connection(
      adapter: "sqlite3",
      database: "db/#{ENV["API_ENV"]}.sqlite3"
    )
    ActiveRecord::Migrator.migrate(File.expand_path('../lib/api/migrations', __FILE__))
  end
end

task :default => :test
