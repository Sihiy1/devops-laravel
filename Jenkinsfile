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
 rm -rf laravel-deploy
 mkdir laravel-deploy
 cp -r $(ls -A | grep -v laravel-deploy) laravel-deploy/
 echo "Deploy ke workspace berhasil"
 '''

 }
}
