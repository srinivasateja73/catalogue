pipeline {
    agent any

    environment {
        COURSE = "Jenkins"
        appVersion = ""
        ACC_ID = "160885265516"
        PROJECT = "roboshop"
        COMPONENT = "catalogue"
    }

    options {
        timeout(time: 10, unit: 'MINUTES')
        disableConcurrentBuilds()
    }

    stages {

        stage('Read Version') {
            steps {
                script {
                    def packageJSON = readJSON file: 'package.json'
                    env.appVersion = packageJSON.version
                    echo "app version: ${env.appVersion}"
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                script{
                sh """
                    npm install
                """
                }
            }

        // stage('Unit Test') {
        //     steps {
        //         sh 'npm test'
        //     }
        // }

        /* stage('Sonar Scan'){
            environment {
                scannerHome = tool 'sonar-8.0'
            }
            steps {
                withSonarQubeEnv('sonar-server') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }

        stage('Quality Gate') {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    waitForQualityGate abortPipeline: true
                }
            }
        } */
    }

    post {
        always {
            echo 'I will always say Hello again!'
            cleanWs()
        }
        success {
            echo 'I will run if success'
        }
        failure {
            echo 'I will run if failure'
        }
        aborted {
            echo 'pipeline is aborted'
        }
    }
}
