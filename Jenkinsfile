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
                sh 'sh bin/setup'
                nodejs('NodeJS-14.10') {
                    sh 'yarn install'
                }
                sh 'sh bin/deploy'
            }
        }
    }
}