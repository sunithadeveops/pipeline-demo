pipeline {
  agent {
        label 'linux'
    }

    stages {
      stage('Maven Build') {
        steps {
          sh 'mvn clean package'
      }
    }
     stage('Deploy to Tomcat') {
      steps {
        sshagent(['tomcat']) {
            // Copy war file to tomcat server
            sh 'scp -o StrictHostKeyChecking=no target/*.war ec2-user@10.20.0.152:/opt/tomcat8/webapps/app.war'
            // stopt tomcat
            sh "ssh ec2-user@10.20.0.152 /opt/tomcat8/bin/shutdown.sh"
            // start tomcat
            sh "ssh ec2-user@10.20.0.152 /opt/tomcat8/bin/startup.sh"
        }
      }
    }
  }
  post {
    success {
      archiveArtifacts artifacts: 'target/*.war'
      cleanWs()
    }
  }
}
