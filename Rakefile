require "rubygems"
require "tmpdir"

require "bundler/setup"
require "jekyll"

require 'html-proofer'

# Change your GitHub reponame
GITHUB_REPONAME = "tadp-utn-frba/tadp-utn-frba.github.io"

desc "Generate blog files"
task :generate do
  Jekyll::Site.new(Jekyll.configuration({
    "source"      => ".",
    "destination" => "_site"
  })).process
end

desc "Check the generated page with html proofer"
task :test do
  begin
    HTMLProofer.check_directory("./_site", {:external_only => true,
                                            :parallel => { :in_processes => 3},
                                            :url_ignore => [/rubymonk.com/, /tadp-utn-frba.github.io/]}).run
  rescue => e
    puts "Task #{task_name} failed"
    puts "#{e.class}: #{e.message}"
  end
  puts "Finished running all tests"

end

desc "Generate and publish blog to gh-pages"
task :publish => [:generate] do
  Dir.mktmpdir do |tmp|
    cp_r "_site/.", tmp

    pwd = Dir.pwd
    Dir.chdir tmp

    system "git init"
    system "git add ."
    message = "Site updated at #{Time.now}"
    system "git commit -m #{message.inspect}"
    system "git remote add origin git@github.com:#{GITHUB_REPONAME}.git"
    system "git push origin master --force"

    Dir.chdir pwd
  end
end
