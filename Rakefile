desc 'deploy static pages to gh-pages'
task :deploy do
  cd('_deploy') { sh 'git pull origin gh-pages' }

  sh 'bundle exec jekyll clean'
  sh 'bundle exec jekyll build'
  sh 'rsync -r --exclude=".git/" --delete _site/ _deploy/'

  cd '_deploy' do
    sh 'git add -A'
    sh 'git commit -v'
    sh 'git push origin gh-pages'
  end
end
