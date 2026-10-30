
pipeline {
    agent any

    triggers {
        pollSCM('H/1 * * * *')
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/vineelagera123-blip/PythonCICD.git'
            }
        }

        stage('Compile') {
            steps {
                bat '"C:\\Users\\vinee\\AppData\\Local\\Programs\\Python\\Python313\\python.exe" -m py_compile app.py'
            }
        }

        stage('Test') {
            steps {
                bat '"C:\\Users\\vinee\\AppData\\Local\\Programs\\Python\\Python313\\python.exe" -m unittest -v'
            }
        }

        stage('Package') {
            steps {
                bat '"C:\\Users\\vinee\\AppData\\Local\\Programs\\Python\\Python313\\python.exe" -m zipfile -c python-app.zip app.py test_app.py'
            }
        }
    }

    post {
        success {
            archiveArtifacts artifacts: 'python-app.zip',
                             fingerprint: true
        }
    }
}
