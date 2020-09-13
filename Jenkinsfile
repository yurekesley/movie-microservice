pipeline {
    agent {
        docker {
            image ' maven:3.6.0-jdk-8-alpine'
            args  '-v /tmp:/tmp'
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
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                '''
            }
        }
        stage('Buildando o projeto com Maven') {
            agent {
                docker {
                    reuseNode true
                    image 'maven:3.6.0-jdk-8-alpine'
                }
            }
            steps {
                withMaven(options: [findbugsPublisher(), junitPublisher(ignoreAttachments: false)]) {
                    sh 'mvn clean $MVN_OPTS package'
                }
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}