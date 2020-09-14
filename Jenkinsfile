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
                echo 'Building..'
                nodejs('NodeJS-14.10') {
                    sh 'yarn install'
                }
                sh 'bin/deploy'
            }
        }
    }
}