pipeline {
    agent any 
    stages {
        stage('Build Image') { 
            steps {
                echo 'Building docker image in local docker library...'
                sh './gradlew bootBuildImage'
            }
        }
        stage('Deploy') { 
            steps {
                echo 'Deploy application to TKGi...'
                
                echo 'Deployment Completed!'
            }
        }
    }
}
