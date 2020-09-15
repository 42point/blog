pipeline {
    agent any
    environment {
        RUBY_HOME="/usr/local/opt/ruby/bin"
        GEM_PATH="/usr/local/opt/ruby/lib/ruby/gems/2.7.0"
        EM_HOME="$GEM_PATH"
        PATH="$RUBY_HOME:$GEM_HOME/bin:$PATH"
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
                echo 'Yarn install'
                nodejs('NodeJS-14.10') {
                    sh 'bin/deploy'
                }
                echo 'Done'
            }
        }
    }
}