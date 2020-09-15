pipeline {
    agent any

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