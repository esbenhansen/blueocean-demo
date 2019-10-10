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
        stash(name: 'testreport', includes: '**/target/surefire-reports/TEST-*.xml,target/*.jar')
      }
    }
    stage('copy artifacts') {
      parallel {
        stage('report') {
          steps {
            tool 'local_artifactory'
            unstash 'testreport'
            junit '**/target/surefire-reports/TEST-*.xml'
          }
        }
        stage('publish') {
          steps {
            unstash 'testreport'
            archiveArtifacts(artifacts: 'target/*.jar', onlyIfSuccessful: true, fingerprint: true)
          }
        }
      }
    }
  }
}