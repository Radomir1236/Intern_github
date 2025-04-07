pipeline {
  agent any
  stages {
    stage ('image_build') {
      steps {
        sh 'touch .env && cat $dot_env > .env'
        sh 'touch Dockerfile && cat $dockerfile > Dockerfile'
        sh 'docker build -t radomir12345/intern:backend_3 .'
        sh 'echo $token_docker | docker login -u $name_hub --password-stdin'
        sh 'docker push radomir12345/intern:backend_3'
        }
      }
    stage ('image_deploy') {
      steps {
        sh 'chmod 600 $Key'
        sh 'ssh -i $Key $Name@$IP_public "yes | docker compose restart backend"'
        sh 'docker image prune -af'
        sh 'docker system prune'
      }
    }
    }
}
