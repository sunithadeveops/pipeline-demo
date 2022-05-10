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
    stage('Deploy to Dev Tomcat') {
      steps {
        tomcatDeploy('13.126.34.96','app','tomcat')
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
