pipeline {
  agent any
  stages {
    stage('BuildStage') {
      steps {
        git(url: 'https://github.com/jenkinsrb/bosrepo1', branch: 'master', credentialsId: '23fe37b6-b0c0-409c-b8ac-11e4a5a4eb81')
        sh '''sudo docker build -t jenkinsrb/jenkinsrepo1:latest .
sudo docker push jenkinsrb/jenkinsrepo1:latest'''
      }
    }

    stage('Dev&QA') {
      parallel {
        stage('DeployDev') {
          steps {
            sh '''sudo docker rm -f $(sudo docker ps -aq)||true
sudo docker run -d -p 7777:80 --name con1 jenkinsrb/jenkinsrepo1:latest'''
          }
        }

        stage('DeployQA') {
          steps {
            echo 'QA deploy done'
          }
        }

      }
    }

  }
}
