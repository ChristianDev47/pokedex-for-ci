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
          image 'node:16'
          args '-u root'
        }
      }
      steps {
        sh 'chown -R 1000:1000 /root/.npm'
        sh "npx browserslist@latest --update-db" 
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