@Library("sharedlibrary") _
 pipeline {
  agent {
        label 'linux1'
    }
    stages {
      stage('Maven Build') {
        steps {
          sh 'mvn clean package'
      }
    }
    stage('Deploy to Tomcat') {
      steps {
        tomcatDeploy('172.31.0.67','app','tomcat')
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
