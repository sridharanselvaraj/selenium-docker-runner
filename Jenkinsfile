pipeline{
  agent any
  stages{
      steps{
          withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'pass', usernameVariable: 'user')]) {
			    sh "docker login --username=${user} --password=${pass}"
			    sh "docker pull srselvaraj/selenium-docker"
        }
      }
      stage("Start Grid"){
        steps{
          sh "docker-compose up -d hub chrome firefox"
        }
      }
      stage("Run Test"){
        steps{
          sh "docker-compose up search-module book-flight-module"
        }
      }
  }
      post{
        always{
           archiveArtifacts artifacts: 'output/**'
           sh "docker-compose down"
        }
      }
}