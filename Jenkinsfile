node {
    checkout scm

    stage("Build") {
        docker.image('composer:2').inside('-u root') {
            sh 'rm -f composer.lock'
            sh 'composer install'
        }
    }

    stage("Testing") {
        docker.image('ubuntu').inside('-u root') {
            sh 'echo "Ini adalah test"'
        }
    }

    stage("Deploy") {
        docker.image('agung3wi/alpine-rsync:1.1').inside('-u root') {
            sshagent(['ssh-prod']) {
                sh '''
                mkdir -p ~/.ssh

                # Hindari host verification error
                ssh -o StrictHostKeyChecking=no bintang@$PROD_HOST "mkdir -p /home/bintang/prod.kelasdevops.xyz"

                # Deploy pakai rsync
                rsync -rav --delete ./ \
                bintang@$PROD_HOST:/home/bintang/prod.kelasdevops.xyz/ \
                --exclude=.env --exclude=storage --exclude=.git \
                -e "ssh -o StrictHostKeyChecking=no"
                '''
            }
        }
    }
}
