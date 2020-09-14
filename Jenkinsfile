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
                echo 'Switch to gh-pages…'
                sh 'if [ `git branch | grep gh-pages` ] then git branch -D gh-pages fi git checkout -b gh-pages'
                echo 'Yarn install'
                nodejs('NodeJS-14.10') {
                    sh 'yarn install --modules-folder ./_assets/yarn'
                }
                echo 'jekyll build'
                sh 'bundle exec jekyll build'
                # sh "find . -maxdepth 1 ! -name '_site' ! -name '.git' ! -name '.gitignore' -exec rm -rf {} \\;"
                # sh 'mv _site/* .'
                # sh 'rm -R _site/'
                # echo 'Deploy..'
            }
        }
    }
}