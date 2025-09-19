pipeline {
  agent any

  environment {
    BUILD_DIR = 'build'
    APP_NAME = 'myapp2'
  }

  stages {
    stage('Checkout') {
      steps {
        // If Jenkinsfile is in this repo and job is Pipeline from SCM, `checkout scm` works.
        // Otherwise you can use `git url: 'https://github.com/you/repo.git', branch: 'main'`
        checkout scm
      }
    }

    stage('Build') {
      steps {
        sh '''
          echo "Preparing build directory..."
          mkdir -p ${BUILD_DIR}
          echo "Simulating build for ${APP_NAME}..."
          echo "build on $(date)" > ${BUILD_DIR}/build-info.txt
        '''
      }
    }

    stage('Unit Tests') {
      steps {
        sh '''
          echo "Running unit tests (simulated)..."
          # replace below with your real test command, e.g. `mvn test` or `npm test`
          sleep 1
          echo "TESTS PASSED" > ${BUILD_DIR}/test-report.txt
        '''
      }
    }

    stage('Archive') {
      steps {
        archiveArtifacts artifacts: "${BUILD_DIR}/**", fingerprint: true
      }
    }
  }

  post {
    success {
      echo "Build succeeded: ${env.BUILD_URL}"
    }
    failure {
      echo "Build failed. Check console output."
    }
    always {
      cleanWs() // requires Workspace Cleanup plugin (commonly installed)
    }
  }
}
