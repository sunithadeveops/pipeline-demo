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
        tomcatDeploy(["10.20.0.152"],"ec2-user","tomcat")
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
