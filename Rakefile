require 'rake'

$LOAD_PATH.unshift('lib')

require 'jeweler'
Jeweler::Tasks.new do |gem|
  gem.name = "jeweler"
  gem.summary = "Simple and opinionated helper for creating Rubygem projects on GitHub"
  gem.email = "josh@technicalpickles.com"
  gem.homepage = "http://github.com/technicalpickles/jeweler"
  gem.description = "Simple and opinionated helper for creating Rubygem projects on GitHub"
  gem.authors = ["Josh Nichols"]
  gem.files.include %w(lib/jeweler/templates/.document lib/jeweler/templates/.gitignore)

  # dependencies defined in Gemfile
end

Jeweler::GemcutterTasks.new

Jeweler::RubyforgeTasks.new do |t|
  t.doc_task = :yardoc
end


require 'rake/testtask'
Rake::TestTask.new(:test) do |test|
  test.test_files = FileList.new('test/**/test_*.rb') do |list|
    list.exclude 'test/test_helper.rb'
  end
  test.libs << 'test'
  test.verbose = true
end

begin
  require 'yard'
  YARD::Rake::YardocTask.new(:yardoc) do |t|
    t.files   = FileList['lib/**/*.rb'].exclude('lib/jeweler/templates/**/*.rb')
  end
rescue LoadError
  task :yardoc => :check_dependencies
end


begin
  require 'rcov/rcovtask'
  Rcov::RcovTask.new(:rcov => :check_dependencies) do |rcov|
    rcov.libs << 'test'
    rcov.pattern = 'test/**/test_*.rb'
  end
rescue
  task :rcov => :check_dependencies
end

begin
  require 'cucumber/rake/task'
  Cucumber::Rake::Task.new(:features) do |features|
    features.cucumber_opts = "features --format progress"
  end
  namespace :features do
    Cucumber::Rake::Task.new(:pretty) do |features|
      features.cucumber_opts = "features --format progress"
    end
  end
rescue LoadError
  task :features => :check_dependencies
  namespace :features do
    task :pretty => :check_dependencies
  end
end

if ENV["RUN_CODE_RUN"] == "true"
  task :default => [:test, :features]
else
  task :default => :test
end


task :test => :check_dependencies
task :features => :check_dependencies


namespace :test do
  task :gemspec_dup do
    gemspec = Rake.application.jeweler.gemspec
    dupped_gemspec = gemspec.dup
    cloned_gemspec = gemspec.clone
    #require 'ruby-debug';breakpoint
    puts gemspec.to_ruby
    puts dupped_gemspec.to_ruby
  end
end
