// Bruno automation demo pipeline
pipeline {
  agent any

  environment {
    NODE_HOME = tool 'Node.js 20'
  }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Install Bruno CLI') {
      steps {
        withEnv(["PATH+NODE=${NODE_HOME}/bin"]) {
          sh 'node -v'
          sh 'npm -v'
          sh 'npm install -g @usebruno/cli'
          sh 'bru --version'
        }
      }
    }

    stage('Run Bruno Demo Checks') {
      steps {
        withEnv(["PATH+NODE=${NODE_HOME}/bin"]) {
          sh '''
            mkdir -p reports
            cd collections/bruno-automation-demo
            bru run \
              --global-env ci \
              --workspace-path ../.. \
              --tags smoke,workflow,release-gate \
              --env-var platform_name="Jenkins" \
              --env-var build_id="${BUILD_NUMBER}" \
              --env-var commit_sha="${GIT_COMMIT}" \
              --reporter-html ../../reports/jenkins-report.html
          '''
        }
      }
    }

    stage('Archive Report') {
      steps {
        archiveArtifacts artifacts: 'reports/*.html', fingerprint: true
      }
    }
  }

  post {
    success {
      echo 'Bruno demo checks passed.'
    }
    failure {
      echo 'Bruno demo checks failed.'
    }
    always {
      echo 'Pipeline finished.'
    }
  }
}
