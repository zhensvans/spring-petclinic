pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        git branch: 'zhensvans-patch-1',
        credentialsId: '5e6ec7ae-355a-4bbb-bccc-490b4b949db3',
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
            cleanWs()
        }
        success {
            emailext (
                to: 'zvardanyan@griddynamics.com',
                subject: "Build Successful: ${currentBuild.fullDisplayName}",
                body: "The build ${currentBuild.fullDisplayName} was successful.\nCheck console output at ${env.BUILD_URL} to view the results."
            )
        }
        failure {
            emailext (
                to: 'zvardanyan@griddynamics.com',
                subject: "Build Failed: ${currentBuild.fullDisplayName}",
                body: "The build ${currentBuild.fullDisplayName} failed.\nCheck console output at ${env.BUILD_URL} to view the results."
            )
        }
    }
}
