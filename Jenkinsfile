pipeline{
    agent any
    tools{
        maven 'maven'
        jdk 'java15'
    }

    stages{
        stage('maven clean'){
            steps{
                bat 'mvn clean'
            }
        }
        stage('maven compile'){
            steps{
                steps{
                    bat 'mvn compile'
                }
            }
        }
        stage('maven tests'){
            steps{
                    bat 'mvn test'
            }
        }

        stage('maven package'){
            steps{
                bat 'mvn package'
            }
        }
    }
}