pipeline {
    agent {
        node {
            label "built-in"
            customWorkspace "/mnt"
        }

    }

    stages {
        stage ("git-cloning-game-of-life-phase-1") {
            steps {
              sh "rm -rf *"
              sh "git clone https://github.com/Lucifer7669/game-of-life.git"
            }
        }

        stage ("building-war-phase-2") {
            steps {
                sh "cd game-of-life && mvn install"
            }
        }

        stage ('docker-compose-execution') {
            steps {
                dir ("/mnt/gameoflife-docker"){
                    sh "git clone https://github.com/Lucifer7669/docker-compose-game-of-life.git"
                    sh "cd docker-compose-game-of-life && docker-compose up -d"
                }
            }
        }
    }
}   