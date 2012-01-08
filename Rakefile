require 'rubygems'
require 'rubygems/gempackagetask'

gemspec = Gem::Specification.new do |s|
  s.name              = 'reportgrid'
  s.version           = '1.0.3'
  s.authors           = ['Kris Nuttycombe']
  s.email             = ['kris [at] reportgrid [dot] com']
  s.homepage          = 'http://api.reportgrid.com/ruby'
  s.rubyforge_project = 'reportgrid'
  s.summary           = 'Ruby client library for ReportGrid (http://www.reportgrid.com)'
  s.description       = File.read(File.expand_path(File.join(File.dirname(__FILE__), 'README.rdoc')))

  s.add_dependency('json')

  s.files = ['Rakefile', 'README.rdoc'] + Dir['lib/*.rb'] + Dir['test/*']
end

task :default => [:test]

task :test do
  Dir[File.expand_path(File.join(File.dirname(__FILE__), 'test', 'test_*'))].each do |test|
    system "ruby #{test} -I #{File.expand_path(File.join(File.dirname(__FILE__), 'lib'))}"
  end
end

task :gemspec do
  gemspec.validate
  File.open("#{gemspec.name}.gemspec", 'w'){|f| f.write gemspec.to_ruby }
end

task :build => :gemspec do
  system "gem build *.gemspec"
  FileUtils.mv "#{gemspec.name}-#{gemspec.version}.gem", "../release/ruby"
end

task :push => :build do
  system "gem push *.gem"
end
