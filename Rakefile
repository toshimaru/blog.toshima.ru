# clone repo:
#   git clone git@github.com:toshimaru/blog.toshima.ru.git -b gh-pages _deploy

desc 'deploy static pages to gh-pages'
task :deploy do
  sh 'bundle exec jekyll clean'
  sh 'bundle exec jekyll build'
  sh 'git add ./docs'
  sh 'git commit -v'
  sh 'git push origin master'
end
