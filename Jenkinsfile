pipeline {
    agent any
    environment {
        PATH = "/usr/share/apache-maven:$PATH"
    }
    stages {
        stage("clone code"){
            steps{
               git credentialsId: 'git_credentials', url: 'https://github.com/stephengrinder/hello-world.git'
            }
        }
        stage("build code"){
            steps{
              sh "mvn clean install"
            }
        }
        stage("deploy"){
            steps{
              sshagent(['Deploy_user']) {
                 sh "scp -o StrictHostKeyChecking=no webapp/target/webapp.war ec2-user@18.207.210.143:/opt/apache-tomcat-8.5.58/webapps"
                 
                }
            }
        }
    }
}
