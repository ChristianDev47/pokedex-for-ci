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
        // Ensure the Jenkins user can write to the npm cache directory
        sh 'mkdir -p /root/.npm'
        sh 'chown -R 1000:1000 /root/.npm'

        // Update Browserslist database
        sh "npx browserslist@latest --update-db"

        // Install dependencies
        sh "npm install"

        // Update specific dependencies (e.g., webpack)
        sh "npm update webpack webpack-cli webpack-dev-server"

        // Build the application
        sh "npm run build"
      }
    }

    stage("Test Application") {
      steps {
        // Run tests
        sh "npm run test"
      }
    }
  }
}
