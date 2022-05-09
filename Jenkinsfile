@Library("sharedlibrary") _
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
    stage('Deploy to Dev Tomcat') {
      steps {
        tomcatDeploy('http://13.126.34.96','app','tomcat-dev')
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
