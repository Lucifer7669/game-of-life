pipeline {
    agent {
        node {
            label "built-in"
            customWorkspace "/mnt/apache-container-pipelines"
        }

    }

    stages {
        stage ('git-cloning-game-of-life-phase-1') {
            steps {
                sh "rm -rf *"
              sh "git clone https://github.com/Lucifer7669/game-of-life.git"
            }
        }

        stage ('building-war-phase-2') {
            steps {
                sh "cd game-of-life && mvn install"
            }
        }

        stage ('creation-of-docker-tomcat-container-phase-3') {
            steps {
                sh "docker run -itdp 80:8080 --name server-tomcat tomcat bash"
            }
        }
        stage ('deployment-war-start-server') {
            steps {
                sh "docker cp game-of-life/gameoflife-web/target/gameoflife.war server-tomcat://usr/local/tomcat/webapps"
            }
        }
    }
}