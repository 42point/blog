pipeline {
    agent any
    environment {
        PATH="/usr/local/opt/ruby/bin:$PATH"
    }
    stages {
        stage('Checkout') {
            steps {
                echo 'Checkout..'
                checkout scm    
            }
        }
        stage('Deploy') {
            steps {
                if [ `git branch | grep gh-pages` ]
                then
                  git branch -D gh-pages
                fi
                  git checkout -b gh-pages

                echo 'node'
                nodejs('NodeJS-14.10') {
                    sh 'yarn install --modules-folder ./_assets/yarn'
                }
                bundle exec jekyll build
                find . -maxdepth 1 ! -name '_site' ! -name '.git' ! -name '.gitignore' -exec rm -rf {} \;
                mv _site/* .
                rm -R _site/
                echo 'Deploy..'
            }
        }
    }
}