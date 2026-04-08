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
  mkdir -p laravel-deploy
  cp -r * laravel-deploy/
  echo "Deploy ke workspace berhasil"
  '''
 }
}
