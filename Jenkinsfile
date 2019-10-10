pipeline {
  agent {
    node {
      label 'master'
    }

  }
  stages {
    stage('build and test') {
      steps {
        tool 'Maven_3_6_2'
        sh '''
            export M2_HOME=/var/jenkins_home/tools/hudson.tasks.Maven_MavenInstallation/Maven_3_6_2
            export M2=$M2_HOME/bin
            export PATH=$M2:$PATH
            mvn -Dmaven.test.failure.ignore clean package

'''
      }
    }
  }
}