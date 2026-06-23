pipeline {
    agent any

    environment {
        ANDROID_HOME = 'C:\\Users\\richa\\AppData\\Local\\Android\\Sdk'
        PATH = "${env.PATH};C:\\Users\\richa\\AppData\\Local\\Android\\Sdk\\platform-tools"
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Baixando o projeto do GitHub...'
                checkout scm
            }
        }

        stage('Verificar ambiente') {
            steps {
                echo 'Verificando versões do ambiente...'
                bat 'node -v'
                bat 'npm -v'
                bat 'java -version'
                bat 'adb version'
                bat 'appium -v'
            }
        }

        stage('Instalar dependências') {
            steps {
                echo 'Instalando dependências do projeto...'
                bat 'npm install'
            }
        }

        stage('Executar testes') {
            steps {
                echo 'Executando script de testes...'
                bat 'npm test'
            }
        }
    }

    post {
        always {
            echo 'Pipeline finalizada.'
        }

        success {
            echo 'Pipeline executada com sucesso.'
        }

        failure {
            echo 'A pipeline falhou. Verifique o console do Jenkins.'
        }
    }
}