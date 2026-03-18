node {
    checkout scm

    stage("Build"){
        docker.image('composer:2').inside('-u root') {
            sh 'composer install'
        }
    }

    stage("Testing"){
        docker.image('ubuntu').inside('-u root') {
            sh 'echo "Ini adalah test"'
        }
    }

    stage("Deploy"){
        docker.image('alpine').inside('-u root') {
            sshagent (credentials: ['ssh-prod']) {
                sh '''
                mkdir -p ~/.ssh
                ssh-keyscan -H 127.0.0.1 >> ~/.ssh/known_hosts

                apk add --no-cache rsync openssh

                rsync -av --delete ./ dymas@127.0.0.1:/home/ubuntu/prod.kelasdevops.xyz/
                '''
            }
        }
    }
}
