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

 stage("Deploy Local"){
  sh '''
  mkdir -p /tmp/laravel-deploy
  cp -r * /tmp/laravel-deploy/
  echo "Deploy local berhasil"
  '''
 }
}
