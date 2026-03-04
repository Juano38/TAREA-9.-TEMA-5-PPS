pipeline {
    agent any

    environment {
        VENV_DIR = "${WORKSPACE}/venv"
    }

    options {
        // Limpiar workspace al inicio para evitar conflictos de builds anteriores
        skipDefaultCheckout(true)
        buildDiscarder(logRotator(numToKeepStr: '10'))
    }

    stages {

        stage('Checkout') {
            steps {
                // Limpieza manual del workspace para evitar conflictos
                deleteDir()

                // Checkout de Git usando credenciales y timeout
                git branch: 'main',
                    url: 'https://github.com/Juano38/TAREA-9.-TEMA-5-PPS.git',
                    credentialsId: 'fec5c479-4745-4666-a6ad-898fdbd2c582'
            }
        }

        stage('Build') {
            steps {
                // Crear virtualenv con pip garantizado e instalar dependencias
                sh '''
            python3 -m venv venv
            . venv/bin/activate
            # Actualizamos pip y solo instalamos si el archivo existe
            pip install --upgrade pip
            if [ -f requirements.txt ]; then
                pip install -r requirements.txt
            else
                echo "Aviso: requirements.txt no encontrado, saltando instalación."
            fi
                '''
            }
        }

        stage('Test') {
            steps {
                // Ejecuta tus tests aquí dentro del virtualenv
                sh '''
                    . "${VENV_DIR}/bin/activate"
                    # Ejemplo: pytest tests/
                    echo "Aquí ejecutarías tus tests"
                '''
            }
        }

        stage('Deploy') {
            steps {
                // Despliegue dentro del virtualenv si es necesario
                sh '''
                    . "${VENV_DIR}/bin/activate"
                    echo "Aquí iría tu despliegue"
                '''
            }
        }
    }

    post {
        failure {
            echo "El pipeline falló. Revisa los logs."
        }
        success {
            echo "Pipeline completado con éxito."
        }
    }
}
