pipeline {
    agent any

    tools {
        allure 'Allure'
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                url: 'https://github.com/AnkitKumar5277/Continous-Testing-Plan.git'
            }
        }

        stage('Check Files') {
            steps {
                bat 'dir'
                bat 'dir postman'
            }
        }

        stage('Run Postman Tests') {
            steps {
                bat '''
                newman run postman/collection.json ^
                -e postman/environment.json ^
                -r allure ^
                --reporter-allure-export allure-results
                '''
            }
        }
    }

    post {
        always {
            allure([
                results: [[path: 'allure-results']]
            ])
        }
    }
}
