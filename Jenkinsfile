pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        git(url: 'https://github.com/jenkinsrb/japp1repo', branch: 'master', credentialsId: 'a6bfc346-d805-4bc9-b607-50473d96e6ec')
        sh '''sudo docker build -t jenkinsrb/buildrepo1:latest .
sudo docker push jenkinsrb/buildrepo1:latest .'''
      }
    }

    stage('ParDeploy') {
      parallel {
        stage('DeployDev') {
          steps {
            sh 'sudo docker run -d -p 7777:8080 jenkinsrb/buildrepo1:latest .'
          }
        }

        stage('DeployQA') {
          steps {
            echo 'QA deployed'
          }
        }

      }
    }

    stage('DeployProd') {
      steps {
        echo 'Prod deploy done!!'
      }
    }

  }
}