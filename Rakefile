require 'rubygems'
require 'rake'

begin
  require 'jeweler'
  Jeweler::Tasks.new do |gem|
    gem.name = "mega_mutex-dalli"
    gem.summary = %Q{Distributed mutex for Ruby using the Dalli memcached client}
    gem.description = %Q{Distributed mutex for Ruby using Dalli memcached client}
    gem.email = "developers@songkick.com"
    gem.homepage = "http://github.com/msaffitz/mega_mutex-dalli"
    gem.authors = ["Matt Johnson", "Matt Wynne", "Michael Saffitz"]
    gem.add_dependency 'dalli', '>= 1.0.0'
    gem.add_dependency 'logging', '>= 1.1.4'
    gem.add_dependency 'retryable', ">= 0.1.0"
    # gem is a Gem::Specification... see http://www.rubygems.org/read/chapter/20 for additional settings
  end
  Jeweler::GemcutterTasks.new
rescue LoadError
  puts "Jeweler (or a dependency) not available. Install it with: sudo gem install jeweler"
end

namespace :github do
  task :push do
    remotes = `git remote`.split("\n")
    unless remotes.include?('github')
      sh('git remote add github git@github.com:msaffitz/mega_mutex-dalli.git')
    end
    sh('git push github master')
  end
end

require 'rspec/core/rake_task'
RSpec::Core::RakeTask.new(:spec) do |spec|
  spec.pattern = 'spec/**/*_spec.rb'
end

RSpec::Core::RakeTask.new(:rcov) do |spec|
  spec.pattern = 'spec/**/*_spec.rb'
  spec.rcov = true
end

task :spec => :check_dependencies

task :default => [:spec, 'github:push', 'gemcutter:release']

require 'rake/rdoctask'
Rake::RDocTask.new do |rdoc|
  if File.exist?('VERSION')
    version = File.read('VERSION')
  else
    version = ""
  end

  rdoc.rdoc_dir = 'rdoc'
  rdoc.title = "mega_mutex-dalli #{version}"
  rdoc.rdoc_files.include('README*')
  rdoc.rdoc_files.include('lib/**/*.rb')
end
