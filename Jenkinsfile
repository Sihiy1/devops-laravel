node {
 checkout scm

 stage("Build"){
  docker.image('composer:2').inside('-u root') {
   sh 'composer install'
  }
 }

 stage("Test"){
  docker.image('ubuntu').inside('-u root') {
   sh 'echo "Ini adalah test"'
  }
 }
}
stage("Deploy"){
 docker.image('alpine:latest').inside('-u root') {
  sshagent (credentials: ['ssh-prod']) {
   sh '''
   apk add --no-cache openssh rsync
   mkdir -p ~/.ssh
   ssh-keyscan -H $PROD_HOST >> ~/.ssh/known_hosts
   rsync -avz . ubuntu@$PROD_HOST:/home/ubuntu/app
   '''
  }
 }
}
