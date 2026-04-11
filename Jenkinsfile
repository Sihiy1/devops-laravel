node {
    checkout scm

    // Build stage
    stage("Build") {
        docker.image('composer:2').inside('-u root') {
            sh 'rm composer.lock'
            sh 'composer install'
        }
    }

    // Testing stage
    stage("Testing") {
        docker.image('ubuntu').inside('-u root') {
            sh 'echo "Ini adalah test"'
        }
    }

    // Deploy stage
    stage("Deploy") {
        docker.image('agung3wi/alpine-rsync:1.1').inside('-u root') {
            sshagent(['ssh-prod-2']) {
                sh 'mkdir -p ~/.ssh'
                sh 'ssh-keyscan -H $PROD_HOST >> ~/.ssh/known_hosts'
                sh '''
                rsync -rav --delete ./ \
                bintang@$PROD_HOST:/home/bashal/prod.kelasdevops.xyz/ \
                --exclude=.env --exclude=storage --exclude=.git
                '''
            }
        }
    }
}
