pipeline {
  agent any
  tools {
    maven 'maven'
  }
  stages{
    stage('1-git-clone'){
      steps{
        checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'git-user', url: 'https://github.com/Etech-Team4/maven-sonar.git']]])
      }
    }
    stage('2-cleanws'){
      steps{
        sh 'mvn clean'
      }
    }
    stage('3-mavenbuild'){
      steps{
        sh 'mvn package'
      }
    }
      stage('unittest'){
        steps{
            sh 'mvn test'
        }
    }
    stage('codequality'){
      steps{
        sh 'mvn clean verify sonar:sonar \
  -Dsonar.projectKey=etech-techops \
  -Dsonar.host.url=http://ec2-13-56-22-125.us-west-1.compute.amazonaws.com:9000 \
  -Dsonar.login=sqp_e65e3af03e8a00b804b81791a1765af5645ecf25'
      }
    }
  }
}
