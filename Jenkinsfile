pipeline {
    agent any

    stages {
        stage ('Compile Stage') {

            steps {
                
                    sh 'mvn clean compile'
                
            }
        }

        stage ('Testing Stage') {

            steps {
                
                    sh 'mvn test'
                
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
                
                    sh 'mvn deploy'
                
            }
        }
    }
}