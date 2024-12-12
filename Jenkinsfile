pipeline {
  agent any
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

    stage("Build Application") {
      agent {
        docker {
          image 'node:latest'
          args '-u root'
        }
      }
      steps {
        sh "npm install"
        sh "npm update webpack webpack-cli webpack-dev-server"
        sh "npm run build"
      }
    }

    stage("Test Application") {
      steps {
        sh "npm run test"
      }
    }
  }
}