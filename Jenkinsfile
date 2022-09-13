pipeline{
    agent any

    tools {
         maven 'maven'
    }

    stages{
        stage('checkout'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'github', url: 'https://github.com/poornima4824/java-jar.git']]])
            }
        }
        stage('build'){
            steps{
               sh 'mvn package'
            }
        }
        stage('Upload Artifacts To Nexus') {
            steps {
                script {
                    nexusArtifactUploader artifacts:
                    [
                        [
                            artifactId: 'jb-hello-world-maven',
                            classifier: '',
                            file: "target/jb-hello-world-maven-0.2.0.jar",
                            type: 'jar'
                        ]
                    ],
                    credentialsId: 'nexus',
                    groupId: 'build',
                    nexusUrl: '3.144.132.81:8081',
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    repository: 'Rollback_mechanism',
                    version: "${GIT_COMMIT}"
                }
            }
        }
    }
}