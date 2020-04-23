
pipeline {
  agent {
    kubernetes {
      yaml """
kind: Pod
metadata:
  name: cloudbees-core
spec:
  containers:
    - name: jdk-8
      image: openjdk:8-jdk-alpine
      command:
        - cat
      tty: true
      workingDir: "/home/jenkins/agent"
"""
    }
  }

  stages {
    stage('Run maven') {
      steps {
             container('jdk-8') {
              sh './mvnw spring-javaformat:apply  && ./mvnw package -Dcheckstyle.skip -DskipTests'
          }
      }
    }
  }
}

