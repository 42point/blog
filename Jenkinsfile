pipeline {
    agent any
    stages {
        stage(`Checkout`) {
            echo 'Checkout..'
        }
        stage('Deploy') {
            steps {
                echo 'Building..'
                sh 'bin/deploy/'
            }
        }
    }
}