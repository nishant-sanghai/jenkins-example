pipeline {
    agent any

    stages {
        stage ('Compile Stage') {

            steps {
                withMaven(maven : 'maven_3_5_0') {
                    sh 'mvn clean compile'
                }
            }
        }

        stage ('Testing Stage') {

            steps {
                withMaven(maven : 'maven_3_5_0') {
                    sh 'mvn test'
                }
            }
            post {
                success {
                    script {
                        skipstages = false
                    }
                    junit 'target/surefire-reports/**/*.xml'
                }
                failure {
                    script {
                        skipstages = true
                    }
                }
            }
        }


        stage ('Deployment Stage') {
            when {
                expression {
                    !skipstages
                }
            }
            steps {
                withMaven(maven : 'maven_3_5_0') {
                    sh 'mvn deploy'
                }
            }
        }
    }
}