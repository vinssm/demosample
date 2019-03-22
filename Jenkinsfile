def AgentName='Linux'
def anyBuildFailed='false'

pipeline {
    agent none
    options {
          skipDefaultCheckout()
    }

    stages {
        stage('Checkout') {
        agent {label "${AgentName}"}
            steps {
                script {
                    deleteDir()
                    checkOutScm()
                    bat 'git clone https://github.com/vinssm/demosample.git'
                }
            }
        }
   //# agent {
    //#    docker {
    //#        image 'maven:3-alpine'
    //#        args '-v /root/.m2:/root/.m2'
    //#    }

        stage('Build') {

            steps {
                sh 'mvn -B -DskipTests clean package'
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
