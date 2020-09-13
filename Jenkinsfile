pipeline {
    def app
    
    agent {
        node {
           label 'master'
        }
    }
   
 environment {
        MAVEN_OPTS= "-XX:+TieredCompilation -XX:TieredStopAtLevel=1 -DdependencyLocationsEnabled=false -Dmaven.repo.local=.m2/repository"
        MVN_OPTS= "-s .m2/settings.xml --batch-mode -DskipTests -DskipITs"
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

        stage('Build image') {
             steps {
                 app = docker.build("yurekesley/movie-microservice")
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