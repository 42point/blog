require 'html-proofer'

task :test do
  sh "bundle exec jekyll build"
  options = { :assume_extension => true }
  HTMLProofer.check_directory("./_site", options).run 
end

task :justtest do
  # options = { :assume_extension => true, :disable_external => true, :check_opengraph => true, :check_html => true}
  options = { :assume_extension => true }
  HTMLProofer.check_directory("./_site", options).run 
end

task :default do
puts "Hello World!"
end


