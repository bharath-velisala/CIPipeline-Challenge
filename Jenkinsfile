pipeline{
    triggers{
        pollSCM('* * * * * *')
    }
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
                bat 'mvn compile'
            }
        }
        stage('maven tests'){
            steps{
                    bat 'mvn test'
            }
        }

        stage('sonar analysis'){
            steps{
                withSonarQubeEnv('sonarcube'){
                    withMaven(maven:'maven'){
                        bat 'mvn sonar:sonar'
                    }
                }
            }

        }
        stage('maven package'){
            steps{
                bat 'mvn package'
            }
        }

        stage('collect artifact'){
     steps{
     archiveArtifacts artifacts: 'target/*.jar', followSymlinks: false
     }
     }

        stage('deploy to artifactory')
     {
     steps{
     
     rtUpload (
    serverId: 'Jfrog',
    spec: '''{
          "files": [
            {
              "pattern": "target/*.jar",
              "target": "mvn-cal"
            }
         ]
    }''',
    buildName: 'holyFrog',
    buildNumber: '1'
)
     }}
    }
}