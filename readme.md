## What is Continuous Testing?
Continous-Testing-Plan-using-Git-Postman-and-Jenkins  
Continuous Testing means **automatically running API tests whenever code changes** using a CI tool.

## 🛠 Tools Used
- Postman – API testing
- Newman – Run Postman tests from command line
- Git – Version control
- Jenkins – CI/CD automation
  
## ▶ How to Run Tests
1. Push Postman tests to GitHub  
2. Jenkins pulls the code  
3. Newman runs API tests  
4. HTML report is generated

# Jenkins Setup:
- Pipeline -> Pipeline script form SCM -> Repo URL
- Branch to Build -> */main
- Create Jenkinsfile -> 🖼️ give screenshot of full opened github project folder structure + this code to llm:

```
pipeline {
    agent any

    tools {
        allure 'Allure'
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: '<your-repo-url>'
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
                jdk: '',
                results: [[path: 'allure-results']]
            ])
        }
    }
}
```

## 📊 Test Report
After Jenkins build:
- Go to Jenkins Job
- Open **Postman API Test Report**
