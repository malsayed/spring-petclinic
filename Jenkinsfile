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
        stage('SonarQube Analysis') {
            steps{
                withSonarQubeEnv(credentialsId: 'SQToken', installationName: 'SonarQube') { // You can override the credential to be used
                    // sh './mvnw org.sonarsource.scanner.maven:sonar-maven-plugin:4.7.0.2747:sonar'
                    sh './mvnw clean package sonar:sonar'
                    
                }
            }
        }

        }
    }
