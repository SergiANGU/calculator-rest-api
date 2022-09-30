pipeline {
    agent any



    stages {
        stage('Build') {
            steps {
                git 'https://github.com/SergiANGU/calculator-rest-api.git'
                sh './mvnw clean compile'
                // bat '.\\mvnw clean compile'
            }
        }
        stage('Test') {
            steps {
                sh "chmod +x -R ${env.WORKSPACE}"
                sh './mvnw test'

                // bat '.\\mvnw test'
            }

            post {
                always {
                junit '**/target/surefire-reports/TEST-*.xml'
                }
            }
        }
        stage('Publish') {
            steps {
                sh './mvnw package'
                // bat '.\\mvnw package'
            }
            post {
                success {
                    archiveArtifacts 'target/*.jar'
                }
            }
        }
    }
}