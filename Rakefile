# Rakefile for Puppet -*- ruby -*-
RAKE_ROOT = File.dirname(__FILE__)

$LOAD_PATH << File.join(RAKE_ROOT, 'tasks')

begin
  require 'rubygems'
  require 'rubygems/package_task'
rescue LoadError
  # Users of older versions of Rake (0.8.7 for example) will not necessarily
  # have rubygems installed, or the newer rubygems package_task for that
  # matter.
  require 'rake/packagetask'
  require 'rake/gempackagetask'
end

require 'rake'

Dir['tasks/**/*.rake'].each { |t| load t }

begin
  load File.join(RAKE_ROOT, 'ext', 'packaging', 'packaging.rake')
rescue LoadError => e
  raise e if ENV['LOAD_ERRORS']
end

build_defs_file = 'ext/build_defaults.yaml'
if File.exist?(build_defs_file)
  begin
    require 'yaml'
    @build_defaults ||= YAML.load_file(build_defs_file)
  rescue StandardError => e
    STDERR.puts "Unable to load yaml from #{build_defs_file}:\n#{e}" if ENV['LOAD_ERRORS']
  end

  @packaging_url  = @build_defaults['packaging_url']
  @packaging_repo = @build_defaults['packaging_repo']
  fail "Could not find packaging url in #{build_defs_file}" if @packaging_url.nil?
  fail "Could not find packaging repo in #{build_defs_file}" if @packaging_repo.nil?

  namespace :package do
    desc 'Bootstrap packaging automation, e.g. clone into packaging repo'
    task :bootstrap do
      if File.exist?("ext/#{@packaging_repo}")
        puts "It looks like you already have ext/#{@packaging_repo}. If you don't like it, blow it away with package:implode."
      else
        cd 'ext' do
          `git clone #{@packaging_url}`
        end
      end
    end
    desc 'Remove all cloned packaging automation'
    task :implode do
      rm_rf "ext/#{@packaging_repo}"
    end
  end
end

task :default do
  sh %(rake -T)
end

task :spec do
  sh %(rspec #{ENV['TEST'] || ENV['TESTS'] || 'spec'})
end

desc 'run style analysis with rubocop'
task(:rubocop) do
  require 'rubocop'
  cli = RuboCop::CLI.new
  cli.run(%w(--display-cop-names --format simple))
end
