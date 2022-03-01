# Add your own tasks in files placed in lib/tasks ending in .rake,
# for example lib/tasks/capistrano.rake, and they will automatically be available to Rake.

require_relative "config/application"

Rails.application.load_tasks

# https://qiita.com/tos-miyake/items/a2e8cde4bff965713e0c

namespace :ridgepole do
  desc 'Apply database schema'
  task apply: :environment do
    ridgepole('--apply', "-E #{Rails.env}", "--file #{schema_file}", "-s animals")
  end

  desc 'Export database schema'
  task export: :environment do
    ridgepole('--export', "-E #{Rails.env}", '--split', "--output #{schema_file}", "-s animals")
  end

  private def schema_file
    Rails.root.join('db/schema/Schemafile') # rubocop:disable Rails/FilePath
  end

  private def config_file
    Rails.root.join('config/database.yml') # rubocop:disable Rails/FilePath
  end

  private def ridgepole(*options)
    command = ['bundle exec ridgepole', "--config #{config_file}"]
    system [command + options].join(' ')
  end
end
