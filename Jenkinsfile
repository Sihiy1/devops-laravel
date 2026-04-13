node {
 checkout scm

 stage("Build"){
  sh 'composer install'
 }

 stage("Test"){
  sh 'echo "Ini adalah test"'
 }

 stage("Deploy") {
    sshagent(['dymas']) {
        sh 'mkdir -p ~/.ssh'
        sh 'ssh-keyscan -H $PROD_HOST >> ~/.ssh/known_hosts'
        sh '''
        rsync -rav --delete ./ \
        dymas@$PROD_HOST:/home/dymas/prod.kelasdevops.xyz/ \
        --exclude=.env --exclude=storage --exclude=.git
        '''
    }
 }
}
