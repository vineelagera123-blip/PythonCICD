
pipeline {
    agent any

    triggers {
        pollSCM('H/1 * * * *')
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
                echo 'Source code checked out from GitHub'
            }
        }

        stage('Compilation') {
            steps {
                bat '"C:\\Users\\vinee\\AppData\\Local\\Programs\\Python\\Python313\\python.exe" -m py_compile app.py'
                echo 'Python syntax check completed'
            }
        }

        stage('Testing') {
            steps {
                bat '"C:\\Users\\vinee\\AppData\\Local\\Programs\\Python\\Python313\\python.exe" -m unittest test_app.py'
            }
        }

        stage('Packaging') {
            steps {
                bat 'powershell.exe -NoProfile -Command "Compress-Archive -Path app.py,test_app.py -DestinationPath python-app.zip -Force"'
            }
        }
    }

    post {
        success {
            archiveArtifacts artifacts: 'python-app.zip'
            echo 'Python CI/CD Pipeline completed successfully!'
        }

        failure {
            echo 'Pipeline failed!'
        }
    }
}
