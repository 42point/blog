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
                sh 'bin/deploy/'
            }
        }
    }
}