pipeline {
    agent any

    tools {
        allure 'Allure'
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/AnkitKumar5277/Continuous-Testing-Plan.git'
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
                includeProperties: false,
                results: [[path: 'allure-results']]
            ])
        }
    }
}
