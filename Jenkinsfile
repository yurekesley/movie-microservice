pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            label 'my-defined-label'
            args  '-v /tmp:/tmp'
        }
    }

    environment {
        MAVEN_OPTS= "-XX:+TieredCompilation -XX:TieredStopAtLevel=1 -DdependencyLocationsEnabled=false -Dmaven.repo.local=.m2/repository"
        MVN_OPTS= "-s .m2/settings.xml --batch-mode -DskipTests -DskipITs"

    }

    tools {
        maven 'M3'
        jdk 'JDK8'
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
        stage('Buldando projeto com Maven') {
            steps {
                echo 'mvn $MVN_OPTS clean package'
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