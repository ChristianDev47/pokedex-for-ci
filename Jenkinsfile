pipeline {
  agent {
    label "jenkins-agent"
  }
  tools {
    maven 'Maven3'
  }
  stages {
    stage("Cleaned Workspace") {
      steps{
        cleanWs()
      }
    } 
    
    stage("Checkout from SCM") {
      steps {
        git branch: 'main', credentialsId: 'github', url: 'https://github.com/ChristianDev47/pokedex-for-ci'
      }
    }
  }
}