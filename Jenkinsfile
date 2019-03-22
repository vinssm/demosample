
pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                    checkout scm
                }
          }

        stage('Build') {

            steps {
                bat 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('deploy') {
            steps {


                sh 'mvn cargo:deploy'
            }
        }
    }
}
