pipeline {
    agent any
    environment{
        BR = "${GIT_BRANCH.split('/').size() > 1 ? GIT_BRANCH.split('/')[1..-1].join('/') : GIT_BRANCH}"
        PRID="${env.CHANGE_ID.split('/').size() > 1 ? env.CHANGE_ID.split('/')[1..-1].join('/') : env.CHANGE_ID}"
        PR="${env.CHANGE_BRANCH.split('/').size() > 1 ? env.CHANGE_BRANCH.split('/')[1..-1].join('/') : env.CHANGE_BRANCH}"
        PRT="${env.CHANGE_TARGET.split('/').size() > 1 ? env.CHANGE_TARGET.split('/')[1..-1].join('/') : env.CHANGE_TARGET}"
        PRTEST="${env.CHANGE_BRANCH}"

    }
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
                    // sh './mvnw clean package sonar:sonar'
                    // sh './mvnw clean package sonar:sonar -Dsonar.branch.name=${BR}'
                    // sh 'git fetch +refs/heads/${CHANGE_TARGET}:refs/remotes/origin/${CHANGE_TARGET}'
                    sh './mvnw clean package sonar:sonar -Dsonar.pullrequest.key=${PRID} -Dsonar.pullrequest.branch=${PR} -Dsonar.pullrequest.base=${PRT} -Dsonar.branch.name=${BR}'
                    sh 'echo ${PRID}'
                    sh 'echo ${PR}'
                    sh 'echo ${PRT}'
                    sh 'echo ${PRTEST}'


                }
            }
        }

        }
    }
