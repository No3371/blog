require 'rake'
require 'date'
require 'yaml'

CONFIG = YAML.load(File.read('_config.yml'))
USERNAME = CONFIG["username"]
REPO = CONFIG["repo"]
DEST_REPO = CONFIG["dest_repo"]
SOURCE_BRANCH = CONFIG["branch"]
DESTINATION_BRANCH = "gh-pages"
CNAME = CONFIG["CNAME"]

namespace :site do
  desc "Generate the site and push changes to remote origin"
  task :deploy do
    repo = Dir.pwd

    # Detect pull request
    if ENV['TRAVIS_PULL_REQUEST'].to_s.to_i > 0
      puts 'Pull request detected. Not proceeding with deploy.'
      exit
    end

    # Configure git if this is run in Travis CI
    if ENV["TRAVIS"]
      sh "git config --global user.name $GIT_NAME"
      sh "git config --global user.email $GIT_EMAIL"
      sh "git config --global push.default simple"
    end

    sh "git remote -v"

    sh "git checkout #{SOURCE_BRANCH}"
    
    # if _site does not exist, clone it
    unless Dir.exist? CONFIG["destination"]
      puts "Destination does not exist: #{Dir.pwd}/#{CONFIG["destination"]}"
      sh "git clone --single-branch --branch #{DESTINATION_BRANCH} https://$GIT_NAME:$GH_TOKEN@github.com/#{USERNAME}/#{DEST_REPO}.git #{CONFIG["destination"]}"
    end

    # # go in to _site and switch to gh_page, note: this is different repo
    # Dir.chdir(CONFIG["destination"])
    # puts "Now at #{Dir.pwd}"

    # Generate the site
    sh "bundle exec jekyll build"
    # Double build for new tags/feeds, as a workaround for now
    # The actual build time is far less then Travis setup time, so it's acceptable
    sh "bundle exec jekyll build"

    # Commit and push to github
    sha = `git log`.match(/[a-z0-9]{40}/)[0]
    Dir.chdir(CONFIG["destination"]) do
      # check if there is anything to add and commit, and pushes it
      puts "Pushing output changes... from #{Dir.pwd}"
      sh "if [ -n '$(git status)' ]; then
            echo '#{CNAME}' > ./CNAME;
            git add --all .;
            git commit -m '(Travis) Updating to #{USERNAME}/#{DEST_REPO}@#{sha}.';
            git push --quiet origin #{DESTINATION_BRANCH};
         fi"
      puts "Pushed updated branch #{DESTINATION_BRANCH} to GitHub Pages"
    end
  end
end
