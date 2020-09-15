pipeline {
    agent any
    environment {
        RUBY_HOME="/usr/local/opt/ruby/bin"
        GEM_PATH="/usr/local/opt/ruby/lib/ruby/gems/2.7.0"
        GEM_HOME="$GEM_PATH"
        PATH="$RUBY_HOME:$GEM_HOME/bin:$PATH"
        LC_ALL = 'en_US.UTF-8'
        LANG    = 'en_US.UTF-8'
        LANGUAGE = 'en_US.UTF-8'
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
                nodejs('NodeJS-14.10') {
                    echo 'Setup…'
                    sh 'bin/setup'
                    echo 'Deploy…'
                    sh 'bin/deploy'
                }
                echo 'Done'
            }
        }
    }
}