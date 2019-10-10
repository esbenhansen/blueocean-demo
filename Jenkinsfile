pipeline {
  agent {
    node {
      label 'master'
    }

  }
  stages {
    stage('build and test') {
      environment {
        M2 = '/var/jenkins_home/tools/hudson.tasks.Maven_MavenInstallation/Maven_3_6_2/bin'
      }
      steps {
        tool 'Maven_3_6_2'
        sh '''$M2/mvn -Dmaven.test.failure.ignore clean package
'''
      }
    }
  }
}