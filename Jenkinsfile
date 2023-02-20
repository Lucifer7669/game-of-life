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
                sh "yum install docker -y"
                sh "service docker start"
                sh "docker run -itdp 80:8080 --name server-tomcat tomcat bash"
            }
        }
        stage ('deployment-war-start-server') {
            steps {
                sh "docker attach server-tomcat"
                sh "bash usr/local/tomcat/bin/startup.sh"
                sh "docker cp game-of-life/gameoflife-web/target/gameoflife.war server-tomcat://usr/local/tomcat/webapps"
                sh "chmod 777 usr/local/tomcat/webapps/*"
            }
        }
    }
}