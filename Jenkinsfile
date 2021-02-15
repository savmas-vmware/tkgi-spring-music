pipeline {
    agent any 
    stages {
        stage('Build Image') { 
            steps {
                echo 'Building docker image in local docker library...'
                sh './gradlew bootBuildImage'
                sh 'docker login -u savmas22 -p Rinku@304'
                sh 'docker tag tkgi-spring-music-pipeline:1.0 savmas22/vmware:tkgi-spring-music-pipeline'
                sh 'docker push savmas22/vmware:tkgi-spring-music-pipeline'
            }
        }
        stage('Deploy') { 
            steps {
                echo 'Deploy application to TKGi...'
                sh '/usr/local/bin/tkgi login -a api.tkgi.platformdemosm.com -u admin -p fcggsq4t8VcrBDxYW-K7Lnl4oi_kWJEk --ca-cert /tmp/ssh/root_ca_cert.pem'
                sh '/usr/local/bin/tkgi get-credentials demo-cluster'
                sh '/usr/local/bin/kubectl apply -f spring-music-deploy.yml'
                sh '/usr/local/bin/kubectl apply -f spring-music-lb-service.yml'
                echo 'Deployment Completed!'
            }
        }
    }
}
