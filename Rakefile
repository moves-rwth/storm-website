require 'html-proofer'

task :test do
  sh "bundle exec jekyll build"
  HTMLProofer.check_directory('_site/', {
    assume_extension: ['.html'],
  }).run
end
