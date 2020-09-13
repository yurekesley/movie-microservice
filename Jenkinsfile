pipeline {
    agent {
        node {
           label 'master'
        }
    }
   
    stages {
        stage ('Verificando variáveis globais') {
            steps {
                sh '''
                    echo "DOCKER_HOME $DOCKER_HOME"
                    echo "DOCKER_HOST $DOCKER_HOST"
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                '''
            }
        }
        stage('Buildando o projeto com Maven') {
            steps {
                 sh 'mvn clean package'
            }
        }
        stage('Criando imagem') {
            steps {
                echo 'docker info'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
