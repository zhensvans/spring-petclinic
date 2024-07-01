pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        git branch: 'zhensvans-patch-1',
        credentialsId: 'github-ssh',
        url: 'git@github.com:zhensvans/spring-petclinic.git/'  
      }
    }

    stage('Build') {
      steps {
        script {
          sh './gradlew build'
        }
      }
    }

    stage('Test') {
      steps {
        script{
          sh './gradlew test'
        }
      }
    }
  }

  post {
    always {
      emailext (
        to: "zvardanyan@griddynamic.com",
        subject: "Jenkins Build ${currentBuild.currentResult}: Job \"${env.JOB_NAME}\"",
        body: "${currentBuild.currentResult}: Job \"${env.JOB_NAME}\" build ${env.BUILD_NUMBER}.\nMore info at: ${env.BUILD_URL}",
        recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']]
      )
    }
  }
}
