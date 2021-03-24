pipeline {
    agent any
    tools { 
        maven 'local' 
    }
    stages {
        stage('Build Application') {
            steps {
                bat 'mvn -f pom.xml test install'
            }
            post {
                success {
                    echo "Now Archiving the Artifacts...."
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }

        stage('Create Tomcat Docker Image'){
            steps {
                sh "pwd"
                sh "ls -a"
                sh "docker build . -t tomcatsamplewebapp:${env.BUILD_ID}"
            }
        }

    }
}
