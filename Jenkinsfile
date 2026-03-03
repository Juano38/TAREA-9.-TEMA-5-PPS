pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', 
                    url: 'https://github.com/Juano38/TAREA-9.-TEMA-5-PPS.git',
                    credentialsId: 'fec5c479-4745-4666-a6ad-898fdbd2c582'
            }
        }

        stage('Build') {
            steps {
                sh 'python3 -m venv venv'
                sh '. venv/bin/activate'
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Test') {
            steps {
                sh 'python3 -m pytest'
            }
        }

        stage('Deploy') {
            steps {
                sh 'echo "Despliegue simulado"'
            }
        }
    }
}
