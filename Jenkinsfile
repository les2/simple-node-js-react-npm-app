pipeline {
    agent {
        docker {
            image 'agencycore/docker-ember-test:latest'
            args '-p 4200:4200'
        }
    }
    environment {
        CI = 'true'
    }
    stages {
        stage('Install Deps') {
            steps {
                sh 'yarn'
            }
        }
        stage('Build') {
            steps {
                sh 'yarn run build'
            }
        }
        stage('Test') {
            steps {
                sh 'yarn run test'
            }
        }
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}
