pipeline {
    agent any 
    stages {
        stage('Build Image') { 
            steps {
                echo 'Delete local image and tag...'
                sh 'docker image rm tkgi-spring-music-pipeline:1.0'
                echo 'Building docker image in local docker library...'
                sh './gradlew bootBuildImage'
                echo 'Push docker image to docker hub...'
                sh 'docker login -u savmas22 -p Rinku@304'
                sh 'docker tag tkgi-spring-music-pipeline:1.0 savmas22/tkgi-spring-music-pipeline:${BUILD_NUMBER}'
                sh 'docker tag tkgi-spring-music-pipeline:1.0 savmas22/tkgi-spring-music-pipeline:latest'
                sh 'docker push savmas22/tkgi-spring-music-pipeline:${BUILD_NUMBER}'
            }
        }
        stage('Deploy') { 
            steps {
                echo 'Deploy application to TKGi...'
                sh '/usr/local/bin/tkgi login -a api.tkgi.platformdemosm.com -u admin -p fcggsq4t8VcrBDxYW-K7Lnl4oi_kWJEk --ca-cert /tmp/ssh/root_ca_cert.pem'
                sh '/usr/local/bin/tkgi get-credentials demo-cluster'
                sh '/usr/local/bin/kubectl apply -f spring-music-deploy.yml'
                sh '/usr/local/bin/kubectl apply -f spring-music-lb-service.yml'
                sh '/usr/local/bin/kubectl set image deployments/spring-music-deploy spring-music-app=savmas22/tkgi-spring-music-pipeline:${BUILD_NUMBER}'
                echo 'Deployment Completed!'
                sh 'docker image rm savmas22/tkgi-spring-music-pipeline:${BUILD_NUMBER}'
            }
        }
    }
}
