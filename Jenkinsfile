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
                
                sh '/usr/local/bin/tkgi get-credentials demo-cluster'
                sh '/usr/local/bin/kubectl apply -f spring-music-deploy.yml'
                echo 'Deployment Completed!'
            }
        }
    }
}
