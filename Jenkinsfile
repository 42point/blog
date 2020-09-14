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
                echo 'node'
                nodejs('NodeJS-14.10') {
                    sh 'yarn install'
                }
                echo 'Deploy..'
                sh 'bin/deploy'
            }
        }
    }
}