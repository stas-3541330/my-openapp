pipeline {
  agent any

  environment {
    KUBECONFIG = credentials('kubeconfig-creds')
    PATH = "/opt/tools:$PATH"
  }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Deploy via Helm') {
      steps {
        sh '''
          helm upgrade --install my-openapp ./helm/my-openapp \
            --namespace my-openapp --create-namespace
        '''
      }
    }

    stage('Verify') {
      steps {
        sh 'kubectl rollout status deployment/my-openapp -n my-openapp'
      }
    }
  }
}

