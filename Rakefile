# Add your own tasks in files placed in lib/tasks ending in .rake,
# for example lib/tasks/capistrano.rake, and they will automatically be available to Rake.

require File.expand_path('../config/application', __FILE__)

Rails.application.load_tasks

stages = [
  :postgres,
  :mysql
]

namespace :dummy do
  stages.each do |stage|
    desc "Test #{stage} dummy app"
    task stage do
      system [
        "RAILS_ENV=#{stage} bundle exec rake db:create",
        "RAILS_ENV=#{stage} bundle exec rake db:dump",
        "RAILS_ENV=#{stage} bundle exec rake db:restore",
        "RAILS_ENV=#{stage} bundle exec cap #{stage} deploy",
        "RAILS_ENV=#{stage} bundle exec cap #{stage} db:pull"
      ].join(" && ") or fail
    end
  end
end

desc "Test dummy apps"
task dummy: stages.map { |stage| "dummy:#{stage}" }
