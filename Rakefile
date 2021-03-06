task :default => [:test]

PKG_NAME = "file-column"
PKG_VERSION = "0.3.2"

PKG_DIR = "release/#{PKG_NAME}-#{PKG_VERSION}"

task :clean do
  rm_rf "release"
end

task :setup_directories do
  mkpath "release"
end


task :checkout_release => :setup_directories do
  rm_rf PKG_DIR
  revision = ENV["REVISION"] || "HEAD"
  sh "svn export -r #{revision} . #{PKG_DIR}"
end

task :release_docs => :checkout_release do
  sh "cd #{PKG_DIR}; rdoc lib"
end

task :package => [:checkout_release, :release_docs] do
  sh "cd release; tar czf #{PKG_NAME}-#{PKG_VERSION}.tar.gz #{PKG_NAME}-#{PKG_VERSION}"
end

task :test do
  sh "cd test; ruby file_column_test.rb"
  sh "cd test; ruby file_column_helper_test.rb"
  sh "cd test; ruby magick_test.rb"
  sh "cd test; ruby magick_view_only_test.rb"
end

require 'jeweler'
Jeweler::Tasks.new do |gem|
  # gem is a Gem::Specification... see http://docs.rubygems.org/read/chapter/20 for more options
  gem.name = "file_column"
  gem.homepage = "http://github.com/tekin/file_column"
  gem.license = "MIT"
  gem.summary = %Q{file upload and rmagick image resizing}
  gem.description = %Q{file upload and rmagick image resizing}
  gem.email = "sebastian.kanthak@muehlheim.de"
  gem.authors = ["Sebastian Kanthak"]
  # dependencies defined in Gemfile
end
Jeweler::RubygemsDotOrgTasks.new