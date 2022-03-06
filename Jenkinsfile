pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                // Run Maven on a Unix agent.
                sh "./mvnw compile"

                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }

            }
        stage('Test') {
            steps {
                // Run Maven on a Unix agent.
                sh "./mvnw test"

                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }

            }
        }
    }
