pipeline {
    agent any

    stages {
        stage('git checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/vigneshak086/ai-leads.git'
            }
        }
        stage('maven build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('tomcat deployment') {
            steps {
                sshagent(['tomcat']) {
                 sh """
                 scp -o StrictHostKeyChecking=no  target/ai-leads.war ec2-user@172.31.17.38:/opt/tomcat10/webapps/
                 ssh ec2-user@172.31.17.38 /opt/tomcat10/bin/shutdown.sh
                 ssh ec2-user@172.31.17.38 /opt/tomcat10/bin/startup.sh
                 """
                }
            }
        }
    }
}
