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
                sh '/usr/local/bin/tkgi login -a api.tkgi.platformdemosm.com -u admin -p fcggsq4t8VcrBDxYW-K7Lnl4oi_kWJEk --ca-cert /home/smascarenhas/ssh/root_ca_cert.pem'
                sh '/usr/local/bin/tkgi get-credentials demo-cluster'
                sh '/usr/local/bin/kubectl apply -f spring-music-deploy.yml'
                echo 'Deployment Completed!'
            }
        }
    }
}
