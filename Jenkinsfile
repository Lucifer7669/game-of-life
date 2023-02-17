pipeline{
    agent {
        label {
            label "built-in" 
            customWorkspace "/mnt/pipeline-jobs/" 
        }
    }
        stages {
            stage ('clone-project'){
                steps{
                   sh "rm -rf *"
                    sh "git clone https://github.com/Lucifer7669/game-of-life.git" 
                }

            }
            stage ('builing-phase'){
                steps {
                     sh "cd game-of-life && mvn install" 
                }
            }
            stage ('deploy-war'){
                steps {   
                sh "scp -i /mnt/key-pair/Jenkins-Installation-script/my-linux.pem game-of-life/gameoflife-web/target/gameoflife.war ec2-user@172.31.45.246:/mnt/server/apache-tomcat-9.0.71/webapps"
                }
            }
           
        }

    
}
