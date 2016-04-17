require "bundler/gem_tasks"
require "rspec/core/rake_task"

RSpec::Core::RakeTask.new(:spec)

task :default => :spec

pwd = File.expand_path('../', __FILE__)

namespace :spec do
  %w(activerecord-40 activerecord-41 activerecord-42 activerecord-50).each do |gemfile|
    desc "Run Tests by #{gemfile}.gemfile"
    task gemfile do
      Bundler.with_clean_env do
        sh "BUNDLE_GEMFILE='#{pwd}/gemfiles/#{gemfile}.gemfile' bundle install --path #{pwd}/.bundle"
        sh "BUNDLE_GEMFILE='#{pwd}/gemfiles/#{gemfile}.gemfile' bundle exec rake -t spec"
      end
    end
  end

  desc "Run All Tests"
  task :all do
    %w(activerecord-40 activerecord-41 activerecord-42 activerecord-50).each do |gemfile|
      Rake::Task["spec:#{gemfile}"].invoke
    end
  end
end
